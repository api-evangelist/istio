---
title: "An Update on Our Container Registry Migration"
url: "https://istio.io/latest/blog/2026/retirement-of-gcr.io-follow-up/"
date: "2026-07-23"
feed_url: "https://istio.io/latest/blog/feed.xml"
---
In a previous blog post , we announced that Istio will retire the gcr.io/istio-release container registry in late 2026 and switch to registry.istio.io/release as the new home for Istio images. The original design was that registry.istio.io/release would be a Cloudflare worker that proxied requests to any OCI-compliant registry, allowing us to switch registries without any interruption to Istio users. Currently, we proxy to gcr.io/istio-release .
