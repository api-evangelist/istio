# Istio

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Istio is an open-source service mesh platform that provides a comprehensive solution for managing, securing, and monitoring microservices in a distributed system. It acts as a middle layer between services, handling communication, routing, and load balancing, as well as providing visibility into the traffic flowing between services. Istio also offers advanced security features such as access control, authentication, and encryption to ensure that communication between services is secure.

**Areas:** Istio · CNCF · Kubernetes · Microservices · Open Source · Service Mesh · Cloud-Native · Graduated

## Istio on APIs.io

Everything profiled for Istio is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/istio/](https://apis.io/providers/istio/)** — or go straight to one of the APIs or properties below.

### APIs (14)

- [Istio Telemetry API](https://apis.io/apis/istio/telemetry-api/) — The Istio Telemetry API (telemetry.istio.io) provides configuration resources for managing observability within an Istio service mesh. The Telemetry…
- [Istio Mesh Config API](https://apis.io/apis/istio/mesh-config-api/) — The Istio Mesh Config API (istio.mesh.v1alpha1) provides global configuration for the Istio service mesh control plane and data plane proxy behavior. It…
- [Istio Operator API](https://apis.io/apis/istio/operator-api/) — The Istio Operator API (istio.operator.v1alpha1) defines the IstioOperator custom resource used to install, configure, and upgrade Istio on Kubernetes…
- [Istio AuthorizationPolicy API](https://apis.io/apis/istio/istio-authorizationpolicy-api/) — Fine-grained access control policies for workloads
- [Istio DestinationRule API](https://apis.io/apis/istio/istio-destinationrule-api/) — Policies applied to traffic after routing (load balancing, connection pool, outlier detection)
- [Istio Gateway API](https://apis.io/apis/istio/istio-gateway-api/) — Load balancer configuration at the edge of the mesh
- [Istio PeerAuthentication API](https://apis.io/apis/istio/istio-peerauthentication-api/) — Mutual TLS configuration for peer-to-peer communication
- [Istio RequestAuthentication API](https://apis.io/apis/istio/istio-requestauthentication-api/) — JWT-based request authentication policies
- [Istio ServiceEntry API](https://apis.io/apis/istio/istio-serviceentry-api/) — External service entries added to the mesh service registry
- [Istio Sidecar API](https://apis.io/apis/istio/istio-sidecar-api/) — Sidecar proxy configuration for inbound and outbound traffic
- [Istio VirtualService API](https://apis.io/apis/istio/istio-virtualservice-api/) — HTTP/TCP routing rules for traffic management
- [Istio WasmPlugin API](https://apis.io/apis/istio/istio-wasmplugin-api/) — WebAssembly plugin configuration for Envoy proxy extensions
- [Istio WorkloadEntry API](https://apis.io/apis/istio/istio-workloadentry-api/) — Non-Kubernetes workload (VM/bare metal) endpoint properties
- [Istio WorkloadGroup API](https://apis.io/apis/istio/istio-workloadgroup-api/) — Collection of workload instances sharing common properties

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Istio Agentic Access](https://apis.io/agentic-access/istio/istio-agentic-access/)

#### JSON Schema (11)

The data models the API reads and writes.

- [Istio AuthorizationPolicy](https://apis.io/schemas/istio/authorization-policy/)
- [Istio DestinationRule](https://apis.io/schemas/istio/destination-rule/)
- [Istio Gateway](https://apis.io/schemas/istio/gateway/)
- [Istio PeerAuthentication](https://apis.io/schemas/istio/peer-authentication/)
- [Istio RequestAuthentication](https://apis.io/schemas/istio/request-authentication/)
- [Istio ServiceEntry](https://apis.io/schemas/istio/service-entry/)
- [Istio Sidecar](https://apis.io/schemas/istio/sidecar/)
- [Istio Telemetry](https://apis.io/schemas/istio/telemetry/)
- [Istio VirtualService](https://apis.io/schemas/istio/virtual-service/)
- [Istio WasmPlugin](https://apis.io/schemas/istio/wasm-plugin/)
- [Istio WorkloadEntry](https://apis.io/schemas/istio/workload-entry/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Istio Context](https://apis.io/jsonld/istio/istio-context/)

#### Collections (15)

Postman and Open Collection request collections.

- [Istio Extensions AuthorizationPolicy API](https://apis.io/collections/istio/open-istio-authorizationpolicy-api/)
- [Istio Extensions AuthorizationPolicy DestinationRule API](https://apis.io/collections/istio/open-istio-destinationrule-api/)
- [Istio Extensions API](https://apis.io/collections/istio/open-istio-extensions-api/)
- [Istio Extensions AuthorizationPolicy Gateway API](https://apis.io/collections/istio/open-istio-gateway-api/)
- [Istio Networking API](https://apis.io/collections/istio/open-istio-networking-api/)
- [Istio Extensions AuthorizationPolicy PeerAuthentication API](https://apis.io/collections/istio/open-istio-peerauthentication-api/)
- [Istio Extensions AuthorizationPolicy RequestAuthentication API](https://apis.io/collections/istio/open-istio-requestauthentication-api/)
- [Istio Security API](https://apis.io/collections/istio/open-istio-security-api/)
- [Istio Extensions AuthorizationPolicy ServiceEntry API](https://apis.io/collections/istio/open-istio-serviceentry-api/)
- [Istio Extensions AuthorizationPolicy Sidecar API](https://apis.io/collections/istio/open-istio-sidecar-api/)
- [Istio Extensions AuthorizationPolicy Telemetry API](https://apis.io/collections/istio/open-istio-telemetry-api/)
- [Istio Extensions AuthorizationPolicy VirtualService API](https://apis.io/collections/istio/open-istio-virtualservice-api/)
- [Istio Extensions AuthorizationPolicy WasmPlugin API](https://apis.io/collections/istio/open-istio-wasmplugin-api/)
- [Istio Extensions AuthorizationPolicy WorkloadEntry API](https://apis.io/collections/istio/open-istio-workloadentry-api/)
- [Istio Extensions AuthorizationPolicy WorkloadGroup API](https://apis.io/collections/istio/open-istio-workloadgroup-api/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Istio — jsonschema rules](https://apis.io/rules/istio/istio-jsonschema-spectral-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Istio Authentication](https://apis.io/security/istio/istio-authentication/)
- [Istio Domain Security](https://apis.io/security/istio/istio-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Istio Plans Pricing](https://apis.io/plans/istio/istio-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Istio Rate Limits](https://apis.io/rate-limits/istio/istio-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Istio Finops](https://apis.io/finops/istio/istio-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://istio.io/)
- [Documentation](https://istio.io/latest/docs/)
- [Getting started](https://istio.io/latest/docs/setup/getting-started/)
- [Support](https://discuss.istio.io/)
- [Changelog](https://github.com/istio/istio/releases)
- [Blog](https://istio.io/latest/blog/)
- [Security](https://istio.io/latest/docs/releases/security-vulnerabilities/)
- [GitHub](https://github.com/istio)

## API Evangelist rating

**Kin Score 34.9** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 64.3 |
| Contract quality | 58.4 |
| Contract governance | 9.8 |
| Operational transparency | 34.2 |
| Developer ergonomics | 38.1 |
| Access clarity | 5.3 |

**Agent readiness 17.9** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | — |
| OpenAPI Examples | — |
| Rate Limit Signal | derived (partial credit) |
| Event Surface Described | — |
| Agent Skills | — |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 16.7** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/istio/](https://apis.io/providers/istio/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Istio: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/istio/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
