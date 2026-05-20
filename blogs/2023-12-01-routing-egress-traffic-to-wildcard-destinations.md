---
title: "Routing egress traffic to wildcard destinations"
url: "https://istio.io/latest/blog/2023/egress-sni/"
date: "Fri, 01 Dec 2023 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
If you are using Istio to handle application-originated traffic to destinations outside of the mesh, you’re probably familiar with the concept of egress gateways. Egress gateways can be used to monitor and forward traffic from mesh-internal applications to locations outside of the mesh. This is a useful feature if your system is operating in a restricted environment and you want to control what can be reached on the public internet from your mesh.
