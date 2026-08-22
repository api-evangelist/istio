# Istio (istio)

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

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/istio/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/istio/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- CNCF
- Kubernetes
- Microservices
- Open Source
- Service Mesh

## Timestamps

- **Created:** 2025-06-05
- **Modified:** 2026-05-19

## APIs

### Istio Networking API

The Istio Networking API (networking.istio.io) provides configuration resources for traffic management within an Istio service mesh.

- **Human URL:** [https://istio.io/latest/docs/reference/config/networking/](https://istio.io/latest/docs/reference/config/networking/)

#### Tags

- Networking
- Service Mesh
- Traffic Management

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/networking/)
- [OpenAPI](openapi/istio-networking-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/istio-networking-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-networking-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/virtual-service.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/destination-rule.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/gateway.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/service-entry.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/sidecar.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/workload-entry.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/istio-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)

### Istio Security API

The Istio Security API (security.istio.io) provides configuration resources for managing security policies within an Istio service mesh. It includes AuthorizationPolicy for fine-grained access control on workloads with ALLOW, DENY, AUDIT, and CUSTOM actions, PeerAuthentication for configuring mutual TLS (mTLS) between service proxies, and RequestAuthentication for validating JWT tokens attached to incoming requests. These resources enforce zero-trust security across the mesh.

- **Human URL:** [https://istio.io/latest/docs/reference/config/security/](https://istio.io/latest/docs/reference/config/security/)

#### Tags

- Authentication
- Authorization
- Security
- Service Mesh

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/security/)
- [OpenAPI](openapi/istio-security-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/istio-security-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-security-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/authorization-policy.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/peer-authentication.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/request-authentication.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/istio-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)

### Istio Telemetry API

The Istio Telemetry API (telemetry.istio.io) provides configuration resources for managing observability within an Istio service mesh. The Telemetry resource enables flexible configuration of metrics, access logs, and distributed tracing for workloads. It uses the concept of providers to indicate the protocol or integration type, and supports fine-grained control over what telemetry data is collected and where it is sent.

- **Human URL:** [https://istio.io/latest/docs/reference/config/telemetry/](https://istio.io/latest/docs/reference/config/telemetry/)

#### Tags

- Metrics
- Observability
- Service Mesh
- Telemetry
- Tracing

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/telemetry/)
- [OpenAPI](openapi/istio-telemetry-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/istio-telemetry-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-telemetry-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/telemetry.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/istio-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)

### Istio Extensions API

The Istio Extensions API (extensions.istio.io) provides configuration resources for extending the Istio service mesh with custom functionality. The WasmPlugin resource enables deploying WebAssembly (Wasm) modules as plugins to the Envoy sidecar proxies, allowing custom processing of network traffic at various phases of the request lifecycle including authentication, authorization, metrics collection, and traffic transformation.

- **Human URL:** [https://istio.io/latest/docs/reference/config/](https://istio.io/latest/docs/reference/config/)

#### Tags

- Extensions
- Service Mesh
- Wasm
- WebAssembly

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/)
- [OpenAPI](openapi/istio-extensions-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/istio-extensions-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-extensions-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/wasm-plugin.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/istio-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)

### Istio Mesh Config API

The Istio Mesh Config API (istio.mesh.v1alpha1) provides global configuration for the Istio service mesh control plane and data plane proxy behavior. It includes MeshConfig for mesh-wide settings such as access logging, tracing providers, and default proxy configuration, as well as ProxyConfig for per-workload proxy tuning and network topology settings. These settings are typically applied via the Istio ConfigMap or as annotations on workloads.

- **Human URL:** [https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/)

#### Tags

- Configuration
- Networking
- Proxy
- Service Mesh

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/)
- [GitHub Repository](https://github.com/istio/api/tree/master/mesh/v1alpha1)
- [Postman Collection](collections/istio-extensions-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-extensions-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/istio-networking-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-networking-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/istio-security-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-security-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/istio-telemetry-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-telemetry-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Istio Operator API

The Istio Operator API (istio.operator.v1alpha1) defines the IstioOperator custom resource used to install, configure, and upgrade Istio on Kubernetes clusters. It provides a declarative interface for selecting Istio profiles, enabling or disabling components such as ingress and egress gateways, and customizing the control plane configuration without editing raw Helm values.

- **Human URL:** [https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/](https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/)

#### Tags

- Installation
- Kubernetes
- Operator
- Service Mesh

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/)
- [GitHub Repository](https://github.com/istio/istio/tree/master/operator)
- [Postman Collection](collections/istio-extensions-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-extensions-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/istio-networking-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-networking-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/istio-security-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-security-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/istio-telemetry-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/istio-telemetry-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/istio)
- [JSON-LD](json-ld/istio-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [JSON Schema](json-schema/virtual-service.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/destination-rule.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/gateway.json) — [JSON Schema](https://json-schema.org/specification)
- [Website](https://istio.io/)
- [Blog](https://istio.io/latest/blog/)
- [News](https://istio.io/latest/news/)
- [Documentation](https://istio.io/latest/docs/)
- [Integrations](https://istio.io/latest/docs/ops/integrations/)
- [Glossary](https://istio.io/latest/docs/reference/glossary/)
- [Git Hub](https://github.com/istio/istio)
- [Git Hub](https://github.com/istio/api)
- [Getting Started](https://istio.io/latest/docs/setup/getting-started/)
- [GitHub Organization](https://github.com/istio)
- [Changelog](https://github.com/istio/istio/releases)
- [Community](https://istio.io/latest/get-involved/)
- [Support](https://discuss.istio.io/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/istio)
- [Security](https://istio.io/latest/docs/releases/security-vulnerabilities/)
- [Issue  Tracker](https://github.com/istio/istio/issues)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
