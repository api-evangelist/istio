---
title: "Introducing the TrafficExtension API"
url: "https://istio.io/latest/blog/2026/traffic-extension-api/"
date: "2026-05-18"
feed_url: "https://istio.io/latest/blog/feed.xml"
---
Mesh extensibility has always been a core tenet of Istio’s design. By allowing users to inject custom logic directly into the data plane, Istio enables a wide range of use cases for performing custom authentication, collecting specialized telemetry, or transforming requests and responses on-the-fly. Until now Istio’s only supported extensibility API was WasmPlugin , which served WebAssembly-based extensions.
