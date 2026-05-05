---
title: "Ambient multi-network multicluster support is now Beta"
url: "https://istio.io/latest/blog/2026/ambient-multinetwork-multicluster-beta/"
date: "Wed, 18 Feb 2026 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
<p>Our team of contributors has been busy throughout the transition to 2026. A lot of work was done to get the multi-network multicluster for ambient to production ready state. Improvements were made in areas from our internal tests, up to the most popular multi-network multicluster asks in ambient, with a big focus on telemetry.</p>
<h2 id="gaps-in-telemetry">Gaps in Telemetry</h2>
<p>The benefits of a multicluster distributed system are not without their tradeoffs. Some complexity is inevitable with larger scale, making good telemetry even more important. The Istio team understands that point and we were aware of some gaps that needed to be covered. Thankfully, on release 1.29, telemetry is now more robust and complete when our ambient data plane operates over distributed clusters and networks.</p>
<p>If you&rsquo;ve deployed alpha multicluster capabilities before in multi-network scenarios, you might have noticed some source or destination labels would show as &ldquo;unknown&rdquo;.</p>
<p>For context, in a local cluster (or clusters sharing the same network), waypoint and ztunnel are aware of all existing endpoints, and they acquire that information through xDS. Confusing metrics instead often occur in multi-network deployments where, given all the information that needs to be replicated across separate networks, the xDS peer discovery is unpractical. Unfortunately, that results in missing peer information when requests traverse network boundaries to reach a different Istio cluster.</p>
<h2 id="telemetry-enhancements">Telemetry Enhancements</h2>
<p>Overcoming that problem, Istio 1.29 now ships with augmented discovery mechanisms in its data plane for exchanging peer metadata between endpoints and gateways sitting across different networks. The HBONE protocol is now enriched with baggage headers, allowing for waypoint and ztunnel to exchange peer information transparently through east-west gateways.</p>
<figure style="width: 100%;">
    <div class="wrapper-with-intrinsic-ratio">
        <a href="/blog/2026/ambient-multinetwork-multicluster-beta/peer-metadata-exchange-diagram.png" title="Diagram showing peer metadata exchange across different networks">
            <img alt="Diagram showing peer metadata exchange across different networks" class="element-to-stretch" src="/blog/2026/ambient-multinetwork-multicluster-beta/peer-metadata-exchange-diagram.png" />
        </a>
    </div>
    <figcaption>Diagram showing peer metadata exchange across different networks</figcaption>
</figure>
<p>In the diagram above, focusing on L7 metrics, we show how the peer metadata flows through baggage headers across different clusters sitting in different networks.</p>
<ol>
<li>The client in Cluster A initiates a request, and ztunnel starts to establish an HBONE connection through the Waypoint. This means ztunnel sends a CONNECT request with a baggage header containing the peer metadata from downstream. That metadata is then stored in the waypoint.</li>
<li>The baggage header containing the metadata is removed, and the request is routed normally. In this case it goes to a different cluster.</li>
<li>On the receiving side, the Ztunnel in Cluster B receives the HBONE request and replies with a successful status, appending a baggage header, now containing the upstream peer metadata.</li>
<li>The upstream peer metadata is invisible to the east-west gateway. And as the response reaches the waypoint, it will now have all the information it needs to emit metrics about the two parties involved.</li>
</ol>
<p>Note that this functionality is behind a feature flag at the moment. If you want to try these telemetry enhancements, they need to be explicitly activated with the <code>AMBIENT_ENABLE_BAGGAGE</code> feature option.</p>
<h2 id="other-improvements-and-fixes">Other Improvements and Fixes</h2>
<p>Some welcomed <a href="/news/releases/1.29.x/announcing-1.29/change-notes/#traffic-management">improvements</a> were made regarding connectivity. Ingress gateways and waypoint proxies can now route requests directly to remote clusters. This sets the stage for easier resiliency and enables more flexible design patterns providing the benefits that Istio users expect in multicluster and multi-network deployments.</p>
<p>And of course, we&rsquo;ve also added a couple of smaller fixes making multi-network multicluster more stable and robust. We&rsquo;ve updated the multicluster documentation to reflect some of these changes, including the addition of a <a href="/docs/ambient/install/multicluster/observability/">guide</a> on how to set up Kiali for an ambient multi-network deployment.</p>
<h2 id="limitations-and-next-steps">Limitations and Next Steps</h2>
<p>All that said, we still acknowledge some gaps weren’t fully covered. Most of the work here was targeting multi-network support. Note that multicluster in single network deployments is still considered alpha stage.</p>
<p>Also, the east-west gateway may give preference to a specific endpoint during a certain time span. This may have some impact on how load from requests coming from a different network is distributed between endpoints. And this is a behavior that impacts both ambient and sidecar data plane modes, and we have plans to address it for both cases.</p>
<p>We’re working with the fantastic Istio community to get these limitations addressed. For now, we’re excited to get this beta out there, and eager to get your feedback. The future is looking bright for Istio multi-network multicluster.</p>
<p>If you would like to try out ambient multi-network multicluster, please follow <a href="/docs/ambient/install/multicluster/multi-primary_multi-network/">this guide</a>. Remember, this feature is in beta status and not ready for production use. We welcome your bug reports, thoughts, comments, and use cases. You can reach us on <a href="https://github.com/istio/istio">GitHub</a> or <a href="https://istio.slack.com/">Slack</a>.</p>
