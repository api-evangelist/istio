---
title: "Retirement of Kubernetes integration jobs for unsupported Kubernetes versions"
url: "https://istio.io/latest/blog/2026/retirement-of-k8s-integration-jobs/"
date: "2026-09-16"
feed_url: "https://istio.io/latest/blog/feed.xml"
---
The Istio Test and Release Working Group is retiring CI integration tests for older Kubernetes versions from the master branch, affecting Istio versions 1.32 and newer. What’s changing Previously, Istio would have a supported range of Kubernetes versions that were typically N-3 or N-4 of the latest Kubernetes version, but would continue testing older Kubernetes versions. Currently, this means we are testing Kubernetes 1.23 through 1.36.
