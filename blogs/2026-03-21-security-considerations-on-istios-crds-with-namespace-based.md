---
title: "Security Considerations on Istio's CRDs with Namespace-based Multi-Tenancy"
url: "https://istio.io/latest/blog/2026/security-considerations-on-namespace-based-multi-tenancy/"
date: "Sat, 21 Mar 2026 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
<p>The Istio project wants to address a possible Man-in-the-Middle (MITM) attack scenario in which a <code>VirtualService</code> can redirect or intercept traffic within the service mesh. This affects namespace-based multi-tenancy clusters where tenants have the permissions to deploy Istio resources (<code>networking.istio.io/v1</code>).</p>
<p>This blog post highlights the risks of using Istio in multi-tenant clusters and explains how users can mitigate these risks and safely operate Istio in their deployments.</p>
<p>Please note that the issues even extend beyond the cluster scope in a <a href="/docs/ops/deployment/deployment-models/#multiple-clusters"><em>&ldquo;single mesh with multiple clusters&rdquo;</em> deployment</a>.</p>
<p>The behavior described in this post applies to Istio version 1.29.0 and to all versions since the introduction of the mesh gateway option in the <code>VirtualService</code> resource.</p>
<h2 id="background">Background</h2>
<h3 id="namespace-based-multi-tenancy">Namespace-based Multi-Tenancy</h3>
<p>Namespaces in Kubernetes provide a mechanism for organizing groups of resources within a cluster. Namespaces provide a logical abstraction that allows teams, applications, or environments to share a single cluster while isolating their resources via controls such as Network Policies, RBAC, and so on.</p>
<p>In this blog post, we focus on running Istio in clusters where multiple tenants share the same cluster and service mesh, and can deploy Istio resources (<code>networking.istio.io/v1</code>) in their namespaces while relying on namespace boundaries for isolation.</p>
<h3 id="traffic-routing-in-istio">Traffic Routing in Istio</h3>
<p>Istio provides traffic management capabilities by separating application logic from network routing behavior.
It introduces additional configuration resources through CRDs that allow operators to define how traffic should be routed between services in the mesh.</p>
<p>One of the central resources for this purpose is the <code>VirtualService</code>. A <code>VirtualService</code> defines a set of routing rules that determine how requests to hosts specified in <code>spec.hosts.[]</code> are handled. These rules can match requests based on properties such as HTTP headers, paths, or ports, and can then direct the traffic to one or more destination services.</p>
<p>Routing decisions defined in a <code>VirtualService</code> are not limited to a single workload or namespace. Depending on how the resource is configured, these rules can affect traffic routing across the entire mesh.</p>
<p>In contrast to the newer <a href="https://gateway-api.sigs.k8s.io/">Kubernetes Gateway API</a>, these CRDs were created and effectively stabilized before namespace-based RBAC even made its way to Kubernetes. Thus, namespace-based multi-tenancy that shares the same service mesh was not part of the threat model at the time. With the introduction of RBAC, such multi-tenant environments emerged. It is therefore important to highlight and address the security risks associated with those architectures.</p>
<p>In the following section, we demonstrate those risks and show that this mechanism can be abused to intercept traffic in a namespace-based multi-tenant cluster. Later, we introduce ways to mitigate those risks.</p>
<h2 id="man-in-the-middle-attacks-through-virtualservice">Man-in-the-Middle Attacks through VirtualService</h2>
<p>In a namespace-based multi-tenant environment, it is often assumed that namespaces provide sufficient trust boundaries between resources across different namespaces. However, Istio’s traffic routing configuration operates at the mesh level, meaning that routing rules defined in one namespace will influence traffic originating from workloads in other namespaces.</p>
<p>An attacker who has permission to create or modify <code>VirtualService</code> resources can abuse this behavior by defining routing rules for arbitrary hosts. When the service mesh parameter <code>mesh</code> is set in the <code>gateways</code> section of the spec, the routing rules are applied to all sidecar proxies in the mesh (independent of their namespace).</p>
<p>This allows an attacker to create a malicious <code>VirtualService</code> that matches requests for specific hostnames and redirects them to an attacker-controlled service. As a result, traffic from other workloads in the mesh can be transparently routed through the attacker’s service before reaching its intended destination.</p>
<p>This behavior enables MITM attacks within the service mesh. The attacker-controlled service can intercept traffic from services in the mesh. This includes traffic to other services in the mesh as well as traffic to the external services. This allows the attacker to:</p>
<ul>
<li>act as the destination service.</li>
<li>redirect traffic to alternative destinations.</li>
<li>drop requests to disrupt the communication (denial-of-service).</li>
</ul>
<p>The source service will send the request to the attacker-controlled service instead of the destination service as the <code>VirtualService</code> overrides the default behavior. Istio&rsquo;s mutual TLS authentication does not help here, because the proxy identifies the attacker-controlled service as the legitimate destination of the overwritten hostname. However, forwarding this traffic to the destination service to read or modify communication between the two services is more challenging for the attacker, as they cannot bypass Istio&rsquo;s <a href="/docs/overview/dataplane-modes/#layer-4-vs-layer-7-features">Layer 4 and Layer 7 security features</a>. As the attacker intercepts the communication, the end-to-end encryption and authentication between the source and the destination service are broken. Thus, the request forwarded from the attacker-controlled service to the destination service is authenticated as a request from the attacker-controlled service. As a result, <a href="/docs/reference/config/security/authorization-policy/">Authorization Policies</a> configured on the destination service may deny the request. In addition, destination service will see the attacker-controlled service identity in the <code>X-Forwarded-Client-Cert</code> header, and the authentication from the source service is lost.</p>
<h2 id="why-does-this-behavior-occur">Why does this behavior occur?</h2>
<p>This behavior results from how Istio distributes and evaluates traffic routing configuration within the service mesh.</p>
<p>Istio service mesh is logically split into a data plane and a control plane. Istio’s control plane aggregates routing configuration from all <code>VirtualService</code> resources and distributes the resulting configuration to the Envoy sidecar proxies that make up the data plane. These proxies then enforce routing rules locally for the traffic they handle, see also <a href="/docs/ops/deployment/architecture/">Istio Architecture</a>.</p>
<p>When a <code>VirtualService</code> is configured as a mesh gateway, its routing rules apply to all sidecars in the mesh, including internal service-to-service traffic. Since the effects of this configuration are not limited to the namespace in which the <code>VirtualService</code> resides, a configuration created in one namespace can match requests originating from workloads in other namespaces.</p>
<h2 id="mitigation-and-best-practices">Mitigation and Best Practices</h2>
<p>Operators running Istio in namespace-based multi-tenancy setups or operating a single mesh across multiple clusters should apply additional safeguards to maintain strong isolation. Without these controls, unintended cross-namespace traffic manipulation can occur at the data plane level.</p>
<h3 id="recommended-mitigation-migrate-to-the-newer-gateway-api">Recommended Mitigation: Migrate to the Newer Gateway API</h3>
<p>Ideally, permissions to create or modify Istio networking resources (<code>networking.istio.io/v1</code> as well as <code>security.istio.io/v1</code>) should be limited to platform operators responsible for global routing.</p>
<p>As an alternative, operators can offer tenants access to the newer <a href="https://gateway-api.sigs.k8s.io/">Gateway API</a>, which was designed with safe cross-namespace support in mind. However, the platform operators still need to control access to shared resources such as gateways.</p>
<p><a href="/docs/ops/configuration/mesh/configuration-scoping/#scoping-mechanisms">Configuration Scoping</a> can be implemented as an additional control.</p>
<h3 id="mitigation-in-legacy-setups">Mitigation in Legacy Setups</h3>
<p>When such changes and restrictions aren’t feasible due to business or organizational requirements, routing configurations should be scoped to specific services or namespaces. Broad rules that affect the entire mesh should be avoided unless explicitly intended, and their implications are well understood.</p>
<p>One way to mitigate this kind of attack is to configure <a href="/docs/ops/configuration/mesh/configuration-scoping/#scoping-mechanisms">Scoping</a>. For instance, to restrict the <a href="/docs/reference/config/networking/sidecar/#IstioEgressListener">Egress listener in every namespace</a> to trusted namespaces. However, this would only mitigate the issue in sidecar mode and ambient mode with waypoints, but not <a href="/docs/ambient/overview/">in L4-only ambient mode</a>, and also not for hosts configured when an <a href="/docs/reference/config/networking/gateway/">Istio Gateway</a> is used.</p>
<p>Another way to mitigate this kind of attack is to implement an <a href="https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/">admission policy</a> that limits which hosts can be used in the <code>host</code> section for each tenant. This will also mitigate the issue in ambient mode.</p>
<h2 id="conclusion">Conclusion</h2>
<p>As shown in this post, Istio’s mesh gateway option allows rules defined in one namespace to affect the traffic of other namespaces. In namespace-based multi-tenancy setups or when running a single mesh across multiple clusters, this behavior may expose the service mesh to malicious actors, e.g., enabling MITM attacks, as explained in this blog post.</p>
<p>Istio does not claim (nor seek to claim) hard namespace-based multi-tenancy as the project chose the tradeoff that eases adoption. Thus, operators who rely on this kind of multi-tenancy should assess the risks involved in their architecture and address the weaknesses, e.g., by removing unnecessary RBAC permissions and enforcing strict admission controls.</p>
<h2 id="references">References</h2>
<ul>
<li><a href="/docs/ops/deployment/security-model/#k8s-account-compromise">Istio Documentation — Security Model</a></li>
<li><a href="/news/security/istio-security-2026-002/">Security Bulletin ISTIO-SECURITY-2026-002</a></li>
<li><a href="/docs/concepts/traffic-management/">Istio Documentation — Traffic Management</a></li>
<li><a href="/docs/reference/config/networking/virtual-service/">Istio Documentation — VirtualService</a></li>
</ul>
