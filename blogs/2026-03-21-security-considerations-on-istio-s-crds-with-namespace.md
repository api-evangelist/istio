---
title: "Security Considerations on Istio's CRDs with Namespace-based Multi-Tenancy"
url: "https://istio.io/latest/blog/2026/security-considerations-on-namespace-based-multi-tenancy/"
date: "Sat, 21 Mar 2026 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
The Istio project wants to address a possible Man-in-the-Middle (MITM) attack scenario in which a VirtualService can redirect or intercept traffic within the service mesh. This affects namespace-based multi-tenancy clusters where tenants have the permissions to deploy Istio resources ( networking.istio.io/v1 ). This blog post highlights the risks of using Istio in multi-tenant clusters and explains how users can mitigate these risks and safely operate Istio in their deployments.
