# Istio (istio)

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
