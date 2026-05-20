---
title: "Istio publishes results of ztunnel security audit"
url: "https://istio.io/latest/blog/2025/ztunnel-security-assessment/"
date: "Fri, 18 Apr 2025 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
Istio’s ambient mode splits the service mesh into two distinct layers: Layer 7 processing (the “ waypoint proxy ”), which remains powered by the traditional Envoy proxy; and a secure overlay (the “zero-trust tunnel” or “ ztunnel ”), which is a new codebase , written from the ground up in Rust. It is our intention that the ztunnel project be safe to install by default in every Kubernetes cluster, and to that end, it needs to be secure and performant. We comprehensively demonstrated ztunnel’s performance, showing that it is the highest-bandwidth way to achieve a secure zero-trust network in…
