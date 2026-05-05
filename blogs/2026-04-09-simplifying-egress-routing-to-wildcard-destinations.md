---
title: "Simplifying Egress Routing to Wildcard Destinations"
url: "https://istio.io/latest/blog/2026/egress-dynamic-dns/"
date: "Thu, 09 Apr 2026 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
<h2 id="overview">Overview</h2>
<p>Controlling egress traffic is a common requirement in service mesh deployments. Many organizations configure their mesh to allow only explicitly registered external services by setting:</p>
<pre><code class="language-plain">meshConfig.outboundTrafficPolicy.mode = REGISTRY_ONLY</code></pre>
<p>With this configuration, any external destination must be registered in the mesh using resources such as <code>ServiceEntry</code> with fully qualified domain names and a DNS resolution type.</p>
<pre><code class="language-yaml">apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
  name: external-wikipedia-https
  namespace: istio-system
spec:
  hosts:
  - "www.wikipedia.org"
  ports:
  - name: tls
    number: 443
    protocol: TLS
  location: MESH_EXTERNAL
  resolution: DNS
  exportTo:
  - "*"</code></pre>
<p>However, some external services expose many dynamic subdomains where applications may need to access endpoints such as:</p>
<pre><code class="language-plain">https://en.wikipedia.org
https://de.wikipedia.org
https://upload.wikipedia.org</code></pre>
<p>As the list of hostnames grows, registering each one individually quickly becomes impractical to manage and scale. To address this, Istio needs support for wildcard hostname registration.</p>
<h2 id="why-wildcard-https-egress-is-difficult">Why wildcard HTTPS egress is difficult</h2>
<p>When a workload initiates an HTTPS connection, the destination hostname is transmitted in the TLS handshake via the <strong>Server Name Indication (SNI)</strong> field.</p>
<p>For example, a client calling <code>https://en.wikipedia.org</code> sends the hostname <code>en.wikipedia.org</code> in the ClientHello SNI field during the TLS handshake. Istio sidecars intercept outbound connections and determine whether the destination is registered and how it should be routed.</p>
<p>However, Istio&rsquo;s routing model normally requires the upstream destination to be known ahead of time. Even if a wildcard match is used in routing rules, the final upstream cluster must still correspond to a statically configured service. Because different subdomains may resolve to different endpoints, routing directly to wildcard hosts was historically not straightforward.</p>
<h2 id="sni-routing-via-egress-gateway">SNI routing via Egress Gateway</h2>
<p>This problem was previously addressed in the Istio blog post <a href="/blog/2023/egress-sni/">Routing egress traffic to wildcard destinations</a>. The architecture included a dedicated egress gateway setup that worked as an SNI forward proxy.</p>
<figure style="width: 90%;">
    <div class="wrapper-with-intrinsic-ratio">
        <a href="/blog/2026/egress-dynamic-dns/egress-sni-flow.svg" title="Egress SNI routing with arbitrary domain names">
            <img alt="Egress SNI routing with arbitrary domain names" class="element-to-stretch" src="/blog/2026/egress-dynamic-dns/egress-sni-flow.svg" />
        </a>
    </div>
    <figcaption>Application → sidecar → egress gateway → SNI inspection → external destination</figcaption>
</figure>
<p>The diagram above was originally published in <a href="/blog/2023/egress-sni/">Routing egress traffic to wildcard destinations</a>.</p>
<p>As shown above:</p>
<ol>
<li>The application initiates an HTTPS connection.</li>
<li>The sidecar proxy intercepts this connection and initiates an internal mTLS connection to the egress gateway.</li>
<li>The gateway terminates this internal mTLS connection.</li>
<li>An internal listener inspects the SNI value from the original TLS handshake.</li>
<li>Traffic is dynamically forwarded to the hostname extracted from SNI.</li>
</ol>
<p>Implementing this required several custom resources:</p>
<ul>
<li><code>ServiceEntry</code> and <code>VirtualService</code> to forward wildcard domain traffic to egress gateway.</li>
<li><code>DestinationRule</code> for mTLS between sidecars and the gateway.</li>
<li><code>EnvoyFilter</code> configuration that enables egress gateway to perform dynamic SNI forwarding, by far the most complex part of this solution. The filter extends the gateway using low-level Envoy capabilities by introducing three pieces: a <strong>patch to the gateway TCP proxy</strong> that routes traffic to an internal listener, an <strong>SNI inspector in the listener</strong> to extract SNI from TLS ClientHello, and a <strong>dynamic forward proxy cluster</strong> for performing dynamic DNS resolution of the SNI.</li>
</ul>
<p>While this approach works, it introduces an additional network hop and an extra layer of internal mTLS for that hop. It also adds operational complexity due to the amount of custom configuration required, which can be difficult to manage and prone to errors. But recent improvements make it possible to achieve the same outcome with a much simpler configuration.</p>
<h2 id="wildcard-serviceentry-with-dynamic_dns-resolution">Wildcard <code>ServiceEntry</code> with <code>DYNAMIC_DNS</code> resolution</h2>
<p>Istio now supports wildcard hostnames with <code>DYNAMIC_DNS</code> resolution in <code>ServiceEntry</code>, enabling sidecar proxies to route wildcard outbound TLS traffic directly without requiring an egress gateway.</p>
<p>For example, the following configuration allows access to all <code>*.wikipedia.org</code> endpoints:</p>
<pre><code class="language-yaml">apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
  name: external-wildcard-https
  namespace: istio-system
spec:
  hosts:
  - "*.wikipedia.org"
  ports:
  - name: tls
    number: 443
    protocol: TLS
  location: MESH_EXTERNAL
  resolution: DYNAMIC_DNS
  exportTo:
  - "*"</code></pre>
<p>Once this resource is applied, workloads in the mesh can connect to any matching subdomain via this ServiceEntry.</p>
<pre><code class="language-bash">$ kubectl exec $POD_NAME -n default -c ratings -- curl -sS -o /dev/null -w "HTTP %{http_code}\n" https://de.wikipedia.org &amp;&amp; echo "Checking stats after request..." &amp;&amp; kubectl exec $POD_NAME -c istio-proxy -- curl -s localhost:15000/clusters | grep "outbound|443||\*\.wikipedia\.org" | grep -E "rq|cx"

HTTP 200
Checking stats after request...
outbound|443||*.wikipedia.org::142.251.223.228:443::cx_active::0
outbound|443||*.wikipedia.org::142.251.223.228:443::cx_connect_fail::0
outbound|443||*.wikipedia.org::142.251.223.228:443::cx_total::3
outbound|443||*.wikipedia.org::142.251.223.228:443::rq_active::0
outbound|443||*.wikipedia.org::142.251.223.228:443::rq_error::0
outbound|443||*.wikipedia.org::142.251.223.228:443::rq_success::0
outbound|443||*.wikipedia.org::142.251.223.228:443::rq_timeout::0
outbound|443||*.wikipedia.org::142.251.223.228:443::rq_total::3</code></pre>
<h3 id="how-the-configuration-works">How the configuration works</h3>
<figure style="width: 90%;">
    <div class="wrapper-with-intrinsic-ratio">
        <a href="/blog/2026/egress-dynamic-dns/egress-dynamic-dns.svg" title="Wildcard ServiceEntry with DYNAMIC_DNS resolution">
            <img alt="Wildcard ServiceEntry with DYNAMIC_DNS resolution" class="element-to-stretch" src="/blog/2026/egress-dynamic-dns/egress-dynamic-dns.svg" />
        </a>
    </div>
    <figcaption>Application → sidecar → external destination</figcaption>
</figure>
<p>A wildcard <code>ServiceEntry</code> with <code>resolution: DYNAMIC_DNS</code> results in Istio creating a <a href="https://www.envoyproxy.io/docs/envoy/latest/api-v3/extensions/clusters/dynamic_forward_proxy/v3/cluster.proto#envoy-v3-api-msg-extensions-clusters-dynamic-forward-proxy-v3-clusterconfig">dynamic forward proxy (DFP)</a> cluster that forwards TLS connections based on the hostname in the SNI field. The wildcard host (for example <code>*.wikipedia.org</code>) is first registered in the mesh service registry, allowing the sidecar to route outbound requests with hostnames matching the pattern. When a workload initiates a TLS connection, SNI Inspector in the listener is configured to read the SNI value from the handshake. The DFP cluster then uses it as the upstream hostname to forward the connection. This effectively enables wildcard HTTPS egress by allowing the proxy to dynamically resolve and forward connections to matching subdomains without requiring static endpoint configuration. All the while, it preserves the client-initiated TLS session, forwarding the encrypted traffic unchanged.</p>
<h2 id="other-use-cases">Other use cases</h2>
<p>This approach is appropriate for use cases where applications need connectivity to wildcard domains while still getting mesh observability and resiliency features.</p>
<h3 id="egress-traffic-in-ambient-mode">Egress traffic in Ambient mode</h3>
<p>In <a href="/docs/ambient/overview/">ambient mesh</a>, node-level ztunnel handles L4 traffic, and an optional <a href="/docs/ambient/usage/waypoint/">waypoint proxy</a> can apply L7 policy and telemetry when explicitly attached. To handle egress through a waypoint, for example to keep a consistent policy path for calls to many AWS service endpoints, the <code>ServiceEntry</code> can be labeled with <code>istio.io/use-waypoint</code> so the control plane directs matching traffic through the named waypoint <code>Gateway</code>.</p>
<p>The example below registers <code>*.amazonaws.com</code> as an external TLS (<code>443</code>) ServiceEntry and pins it to a waypoint gateway named <code>waypoint</code>:</p>
<pre><code class="language-yaml">apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
  name: amazonaws-wildcard
  namespace: istio-system
  labels:
    istio.io/use-waypoint: waypoint # attached to a waypoint gateway
spec:
  exportTo:
  - .
  hosts:
  - '*.amazonaws.com'
  location: MESH_EXTERNAL
  ports:
  - name: tls
    number: 443
    protocol: TLS
  resolution: DYNAMIC_DNS</code></pre>
<h3 id="traffic-to-unknown-internal-destinations">Traffic to unknown internal destinations</h3>
<p>A caller may only have a limited number of services in its config but still need mTLS connectivity to other internal services. The setup is:</p>
<ul>
<li>A <code>Sidecar</code> resource that limits the ratings service egress hosts to the <code>istio-system</code> namespace, i.e., it cannot call the details service directly:</li>
</ul>
<pre><code class="language-yaml">apiVersion: networking.istio.io/v1
kind: Sidecar
metadata:
  name: restrict-default
  namespace: default
spec:
  workloadSelector:
    labels:
      app: ratings
  egress:
  - hosts:
    - "istio-system/*"</code></pre>
<ul>
<li><code>ServiceEntry</code> that defines wildcard service for other internal services:</li>
</ul>
<pre><code class="language-yaml">apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
  name: internal-wildcard-http
  namespace: istio-system
spec:
  hosts:
  - "*.svc.cluster.local"
  ports:
  - name: http
    number: 9080
    protocol: HTTP
  location: MESH_INTERNAL
  resolution: DYNAMIC_DNS
  exportTo:
  - "*"</code></pre>
<ul>
<li><code>DestinationRule</code> that defines mTLS configuration for this <code>ServiceEntry</code>:</li>
</ul>
<pre><code class="language-yaml">apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
  name: internal-wildcard-dr
  namespace: istio-system
spec:
  host: "*.svc.cluster.local"
  trafficPolicy:
    tls:
      mode: MUTUAL_TLS # needs DNS SAN in cert
  exportTo:
  - "*"</code></pre>
<p>Ratings service can now call other services in the mesh, even though it doesn&rsquo;t have them in its config, by resolving the hostname dynamically using DNS:</p>
<pre><code class="language-bash">$ kubectl exec $POD_NAME -n default -c ratings -- curl -sS -o /dev/null -w "HTTP %{http_code}\n" details.default.svc.cluster.local:9080/details/0 &amp;&amp; echo "Checking stats after request..." &amp;&amp; kubectl exec $POD_NAME -c istio-proxy -- curl -s localhost:15000/clusters | grep "outbound|9080||\*\.svc\.cluster\.local" | grep -E "rq_total|rq_success"

Making test request...
HTTP 200
Checking stats after request...
outbound|9080||*.svc.cluster.local::10.96.35.238:9080::rq_success::1
outbound|9080||*.svc.cluster.local::10.96.35.238:9080::rq_total::1</code></pre>
<p>Note: mTLS in this use case needs the certs to have DNS SANs since Envoy&rsquo;s dynamic forward proxy leverages hostname to perform auto SAN validation.</p>
<h2 id="conclusion">Conclusion</h2>
<p>Istio sidecar proxies can now directly handle HTTP and TLS egress traffic to wildcard domains with the introduction of wildcard <code>ServiceEntry</code> support and <code>DYNAMIC_DNS</code> resolution. This enables simpler configuration and a more direct request path, reducing latency by removing the need for an intermediate egress gateway hop, while still preserving the existing security and policy controls.</p>
<h2 id="references">References</h2>
<ul>
<li><a href="/blog/2023/egress-sni/">Routing egress traffic to wildcard destinations</a></li>
<li><a href="https://www.envoyproxy.io/docs/envoy/latest/configuration/listeners/network_filters/sni_dynamic_forward_proxy_filter">SNI dynamic forward proxy - Envoy documentation</a></li>
<li><a href="https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/http/http_proxy#arch-overview-http-dynamic-forward-proxy">HTTP dynamic forward proxy - Envoy documentation</a></li>
</ul>
