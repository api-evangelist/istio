# Istio (istio)
Istio is an open-source service mesh platform that provides a comprehensive solution for managing, securing, and monitoring microservices in a distributed system. It acts as a middle layer between services, handling communication, routing, and load balancing, as well as providing visibility into the traffic flowing between services. Istio also offers advanced security features such as access control, authentication, and encryption to ensure that communication between services is secure. By centralizing these functionalities, Istio simplifies the complexity of managing a microservices architecture and allows developers to focus on building and deploying their applications without having to worry about the underlying infrastructure.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/istio/refs/heads/main/apis.yml)

## Scope

- **Type:** Index 
- **Position:** Consuming 
- **Access:** 3rd-Party 

## Tags:

 - Service Mesh

## Timestamps

- **Created:** 2025-06-05 
- **Modified:** 2026-03-18 

## APIs

### Istio Networking API
The Istio Networking API (networking.istio.io) provides configuration resources for traffic management within an Istio service mesh. It includes VirtualService for HTTP/TCP routing rules, DestinationRule for load balancing and connection pool settings, Gateway for managing inbound and outbound traffic at the mesh edge, ServiceEntry for adding external services to the mesh registry, Sidecar for controlling network reachability of sidecar proxies, WorkloadEntry and WorkloadGroup for non-Kubernetes workloads such as VMs, and ProxyConfig for per-workload proxy configuration. These resources are defined as Kubernetes Custom Resource Definitions (CRDs) and accessed via the Kubernetes API server.

**Human URL:** [https://istio.io/latest/docs/reference/config/networking/](https://istio.io/latest/docs/reference/config/networking/)


#### Tags:

 - Service Mesh, Traffic Management, Networking

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/networking/)
- [OpenAPI](openapi/istio-networking-api-openapi.yml)
- [JSONSchema](json-schema/virtual-service.json)
- [JSONSchema](json-schema/destination-rule.json)
- [JSONSchema](json-schema/gateway.json)
- [JSONSchema](json-schema/service-entry.json)
- [JSONSchema](json-schema/sidecar.json)
- [JSONSchema](json-schema/workload-entry.json)
- [JSONLD](json-ld/istio-context.jsonld)

### Istio Security API
The Istio Security API (security.istio.io) provides configuration resources for managing security policies within an Istio service mesh. It includes AuthorizationPolicy for fine-grained access control on workloads with ALLOW, DENY, AUDIT, and CUSTOM actions, PeerAuthentication for configuring mutual TLS (mTLS) between service proxies, and RequestAuthentication for validating JWT tokens attached to incoming requests. These resources enforce zero-trust security across the mesh.

**Human URL:** [https://istio.io/latest/docs/reference/config/security/](https://istio.io/latest/docs/reference/config/security/)


#### Tags:

 - Service Mesh, Security, Authentication, Authorization

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/security/)
- [OpenAPI](openapi/istio-security-api-openapi.yml)
- [JSONSchema](json-schema/authorization-policy.json)
- [JSONSchema](json-schema/peer-authentication.json)
- [JSONSchema](json-schema/request-authentication.json)
- [JSONLD](json-ld/istio-context.jsonld)

### Istio Telemetry API
The Istio Telemetry API (telemetry.istio.io) provides configuration resources for managing observability within an Istio service mesh. The Telemetry resource enables flexible configuration of metrics, access logs, and distributed tracing for workloads. It uses the concept of providers to indicate the protocol or integration type, and supports fine-grained control over what telemetry data is collected and where it is sent.

**Human URL:** [https://istio.io/latest/docs/reference/config/telemetry/](https://istio.io/latest/docs/reference/config/telemetry/)


#### Tags:

 - Service Mesh, Telemetry, Observability, Metrics, Tracing

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/telemetry/)
- [OpenAPI](openapi/istio-telemetry-api-openapi.yml)
- [JSONSchema](json-schema/telemetry.json)
- [JSONLD](json-ld/istio-context.jsonld)

### Istio Extensions API
The Istio Extensions API (extensions.istio.io) provides configuration resources for extending the Istio service mesh with custom functionality. The WasmPlugin resource enables deploying WebAssembly (Wasm) modules as plugins to the Envoy sidecar proxies, allowing custom processing of network traffic at various phases of the request lifecycle including authentication, authorization, metrics collection, and traffic transformation.

**Human URL:** [https://istio.io/latest/docs/reference/config/](https://istio.io/latest/docs/reference/config/)


#### Tags:

 - Service Mesh, Extensions, WebAssembly, Wasm

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/)
- [OpenAPI](openapi/istio-extensions-api-openapi.yml)
- [JSONSchema](json-schema/wasm-plugin.json)
- [JSONLD](json-ld/istio-context.jsonld)

### Istio Mesh Config API
The Istio Mesh Config API (istio.mesh.v1alpha1) provides global configuration for the Istio service mesh control plane and data plane proxy behavior. It includes MeshConfig for mesh-wide settings such as access logging, tracing providers, and default proxy configuration, as well as ProxyConfig for per-workload proxy tuning and network topology settings. These settings are typically applied via the Istio ConfigMap or as annotations on workloads.

**Human URL:** [https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/)


#### Tags:

 - Service Mesh, Configuration, Proxy, Networking

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/)
- [GitHubRepository](https://github.com/istio/api/tree/master/mesh/v1alpha1)

### Istio Operator API
The Istio Operator API (istio.operator.v1alpha1) defines the IstioOperator custom resource used to install, configure, and upgrade Istio on Kubernetes clusters. It provides a declarative interface for selecting Istio profiles, enabling or disabling components such as ingress and egress gateways, and customizing the control plane configuration without editing raw Helm values.

**Human URL:** [https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/](https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/)


#### Tags:

 - Service Mesh, Operator, Installation, Kubernetes

#### Properties

- [Documentation](https://istio.io/latest/docs/reference/config/istio.operator.v1alpha1/)
- [GitHubRepository](https://github.com/istio/istio/tree/master/operator)

## Common Properties

- [JSON-LD](json-ld/istio-context.jsonld)
- [JSONSchema](json-schema/virtual-service.json)
- [JSONSchema](json-schema/destination-rule.json)
- [JSONSchema](json-schema/gateway.json)
- [Website](https://istio.io/)
- [Blog](https://istio.io/latest/blog/)
- [News](https://istio.io/latest/news/)
- [Documentation](https://istio.io/latest/docs/)
- [Integrations](https://istio.io/latest/docs/ops/integrations/)
- [Glossary](https://istio.io/latest/docs/reference/glossary/)
- [GitHub](https://github.com/istio/istio)
- [GitHub](https://github.com/istio/api)
- [Getting Started](https://istio.io/latest/docs/setup/getting-started/)
- [GitHub Organization](https://github.com/istio)
- [Change Log](https://github.com/istio/istio/releases)
- [Community](https://istio.io/latest/get-involved/)
- [Support](https://discuss.istio.io/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/istio)
- [Security](https://istio.io/latest/docs/releases/security-vulnerabilities/)
- [Issue Tracker](https://github.com/istio/istio/issues)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
