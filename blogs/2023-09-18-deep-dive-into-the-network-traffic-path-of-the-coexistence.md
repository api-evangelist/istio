---
title: "Deep Dive into the Network Traffic Path of the Coexistence of Ambient and Sidecar"
url: "https://istio.io/latest/blog/2023/traffic-for-ambient-and-sidecar/"
date: "Mon, 18 Sep 2023 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
Ambient mode now uses in-Pod redirection to redirect traffic between workload pods and ztunnel. The method described in this blog is no longer needed, and this post has been left for historical interest. There are 2 deployment modes for Istio: ambient mode and sidecar mode.
