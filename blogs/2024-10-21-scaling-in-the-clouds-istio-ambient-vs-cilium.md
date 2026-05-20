---
title: "Scaling in the Clouds: Istio Ambient vs. Cilium"
url: "https://istio.io/latest/blog/2024/ambient-vs-cilium/"
date: "Mon, 21 Oct 2024 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
A common question from prospective Istio users is “how does Istio compare to Cilium?” While Cilium originally only provided L3/L4 functionality, including network policy, recent releases have added service mesh functionality using Envoy, as well as WireGuard encryption. Like Istio, Cilium is a CNCF Graduated project, and has been around in the community for many years. Despite offering a similar feature set on the surface, the two projects have substantially different architectures, most notably Cilium’s use of eBPF and WireGuard for processing and encrypting L4 traffic in the kernel,…
