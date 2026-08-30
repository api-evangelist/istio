---
title: "ACTION REQUIRED FOR GOOGLE CONTAINER REGISTRY USERS, scream tests, and our move to AWS"
url: "https://istio.io/latest/blog/2026/retirement-of-gcp/"
date: "2026-08-21"
feed_url: "https://istio.io/latest/blog/feed.xml"
---
This year, Istio is migrating all of our infrastructure from Google Cloud Platform to Amazon Web Services due to changes in our funding model. This post describes the transition of our container images, Helm charts, other release artifacts (RPMs, DEBs, source code, SPDX documents, istioctl , and licenses), signing keys, and upcoming scream tests where we will disable access to all GCP-hosted artifacts . Container Images In a previous blog post , we announced that the gcr.io/istio-release and registry.istio.io container registries will be decommissioned in December 2026 and we would only publis
