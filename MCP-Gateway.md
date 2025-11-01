| Metadata | Value |
|----------|-------|
| **Title** | MCP Gateway Criteria |
| **Description** | Criteria and guidelines for implementing an MCP Gateway |
| **Status** | Draft |
| **Version** | 0.0.1 |
| **Author** | Andor Kesselman (andor@agentoverlay.com) |

## Introduction

The **Model Context Protocol (MCP)** ecosystem has expanded rapidly over the past year. Many organizations are now experimenting with **MCP Gateways**—specialized infrastructure layers that standardize how autonomous agents discover and call tools, securely connect to external services, and enforce enterprise policies.

An **MCP Gateway** acts as a trusted intermediary between agents and the broader network of tools and data sources. It provides a common interface for tool registration and discovery, manages context passing between agents and environments, and applies governance controls such as authentication, authorization, logging, and rate limiting. In enterprise deployments, the gateway often doubles as a reverse proxy, ensuring that agent interactions comply with internal security, privacy, and compliance policies while maintaining performance and observability.

To help readers navigate this fast-evolving space, the **evaluation framework** below scores each gateway across six major categories:

1. **Core MCP Capabilities**
2. **Security and Compliance**
3. **Performance and Scalability**
4. **Operations and Reliability**
5. **Developer Experience**
6. **Architecture and Integration**

Each criterion is weighted by priority: *must-have (P0)* features carry triple weight, *should-have (P1)* features double weight, and *nice-to-have (P2)* features single weight. Scores range from **0 (unsupported)** to **3 (enterprise-grade)**, with higher totals indicating more mature and production-ready offerings.

## High Level Architecture 

The **MCP Gateway** serves as the central coordination and control layer within the Model Context Protocol ecosystem. It manages how autonomous agents (MCP Clients) interact with tools and services (MCP Servers), defining clear trust boundaries both inside and outside an organization. In essence, it is the **policy and routing hub** for all agentic traffic—governing what can talk to what, under which conditions, and with what level of visibility.

<img width="1748" height="1136" alt="image" src="https://gist.github.com/user-attachments/assets/ddc19259-21a9-40e9-b470-d4c2619d98f6" />

As shown in the high-level architecture diagram, an MCP Gateway typically sits between hosted MCP Servers and the clients that use them. Within an enterprise, this allows the gateway to function as an **internal trust boundary**, unifying multiple servers into a single access layer. All requests from agents—whether they involve querying data, invoking tools, or retrieving contextual information—flow through the gateway, where they can be authenticated, authorized, and observed in real time. This ensures that internal systems remain consistent and compliant without slowing down innovation or experimentation.

At the same time, the gateway also manages the **external boundary** of an organization’s trust domain. It acts as the secure bridge to external partners, ecosystems, or marketplaces of MCP clients and servers. By brokering these cross-boundary interactions, the gateway can apply enterprise policy—such as filtering prompts, enforcing rate limits, or anonymizing data—before information leaves the internal network. This dual role makes the MCP Gateway a foundational piece of infrastructure for enterprises that want to safely participate in the emerging, interconnected agent economy.

<img width="954" height="1246" alt="image" src="https://gist.github.com/user-attachments/assets/727a628d-a008-4dd4-99ec-3ec4ed387651" />

Beneath this architectural layer lies a rich set of **capabilities**. The gateway maintains a **registry** of available servers and tools, allowing agents to discover and bind to them dynamically. It handles **authentication and authorization (AuthN/AuthZ)**, ensuring only approved entities can access sensitive resources. It performs **translations** between schemas or tool definitions to preserve interoperability, and provides **observability** across all interactions for auditing and performance tuning. Other capabilities include **routing and proxying**, **networking controls**, **virtual server orchestration**, **LLM testing**, and **prompt filtering**—each adding another layer of safety, control, and insight.

Together, these features make the MCP Gateway far more than a traffic router. It is the **governance and policy enforcement point** of the Model Context Protocol—enabling enterprises to control both the surface area and behavior of their agent networks while maintaining trust, compliance, and performance at scale.

## Criteria Considerations

To objectively assess the maturity and enterprise readiness of MCP Gateways, a consistent set of evaluation criteria is used. Each category captures a distinct dimension of gateway capability — from core protocol adherence and agent orchestration to compliance posture, scalability, and developer ergonomics.

These criteria are not merely technical benchmarks; they represent the practical considerations that determine whether an MCP Gateway can operate reliably in complex, real-world environments. By defining these categories, evaluators can score each solution along comparable axes, identify trade-offs, and highlight differentiators among competing implementations.

We describe how to score each category relative to your use case in the [Scoring](#scoring-methodology) section

### Scoring Methodology

To score, each MCP Gateway is evaluated against the defined criteria using a weighted scoring system designed to balance functional depth with enterprise readiness. The framework quantifies both **feature completeness** and **implementation maturity**, allowing for consistent comparison across diverse gateway architectures.

Each capability within a category is scored on a **0–3 scale**, where higher values indicate greater robustness, integration depth, and production readiness:

| **Score**                | **Meaning**                                                                                                                        |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| **0 – Unsupported**      | The feature is not available or not applicable within the current implementation.                                                  |
| **1 – Experimental**     | Early or partial support exists but lacks stability, documentation, or enterprise reliability.                                     |
| **2 – Production-Ready** | The feature is well implemented, stable, and documented; sufficient for most enterprise use cases.                                 |
| **3 – Enterprise-Grade** | The feature is fully matured, extensible, and optimized for scale, with strong compliance, observability, and integration support. |

To account for varying importance across features, each capability is assigned a **priority weight**:

* **P0 (Must-Have)** → ×3 weight
* **P1 (Should-Have)** → ×2 weight
* **P2 (Nice-to-Have)** → ×1 weight

Defaults may be chosen by industry alignment, but your organization may have it's own requirements and may decide to weigh each of the priorities differently. 

The **total score** for a gateway is computed as the weighted sum of all category scores, normalized to produce an aggregate rating that reflects overall maturity and alignment with enterprise needs. This allows readers to identify strengths and trade-offs—for example, a gateway with strong developer experience but limited compliance features—while maintaining transparency in how evaluations are derived.

### High Level Categories

| **Code** | **Category**                                | **Description**                                                                                                                                                                                                                                                                                                                                    |
| -------- | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **C1**   | **Core Protocol & Agent Logic**             | Evaluates how well the gateway implements MCP primitives and supports core agent operations. Includes tool transformation (REST/gRPC), function integration, registry management, universal LLM abstraction, and multi-agent orchestration capabilities.                                                                                           |
| **C2**   | **Security & Compliance**                   | Assesses the gateway’s ability to enforce secure and compliant operations through strong authentication and authorization (AuthN/AuthZ), SSO integration, and guardrails for prompt injection or PII redaction. Also considers alignment with regulatory frameworks such as GDPR and HIPAA, audit logging, and adherence to zero-trust principles. |
| **C3**   | **Performance & Scalability**               | Measures how effectively the gateway handles high-load scenarios and large-scale deployments. Includes metrics for latency, throughput, horizontal scaling, streaming support, failover behavior, rate limiting, and high availability (HA).                                                                                                       |
| **C4**   | **Operations & Reliability**                | Covers deployment flexibility, monitoring, observability, and fault-tolerance mechanisms. Focuses on how consistently and predictably the gateway can operate in production environments under varying workloads.                                                                                                                                  |
| **C5**   | **Developer Experience**                    | Examines the ergonomics, tooling, and documentation available to developers integrating or extending the gateway. Considers the ease of setup, debugging, configuration, and local testing, as well as quality of SDKs, CLIs, and APIs.                                                                                                            |
| **C6**   | **Architecture, Licensing & Extensibility** | Analyzes deployment and licensing models (SaaS, self-hosted, or private cloud), open-source versus proprietary availability, plugin and extension models, API-first design, and the overall extensibility of the platform.                                                                                                                         |

### Sub-Categories

| Category | Criterion | Description | Considerations |
| ----- | ----- | ----- | ----- |
| Core Protocol & Agent Logic | Full MCP Compliance | Ensures interoperability with the MCP protocol and agents across different implementations. | Check support for latest MCP spec and primitives such as tasks, resource streaming and tool invocation. |
| Core Protocol & Agent Logic | Server Registry | A central catalog that registers available MCP servers and tools. | Look for dynamic registration, capability discovery, and API to list tools. |
| Core Protocol & Agent Logic | Federation | Allows composition of multiple servers into a unified namespace. | Check for virtual servers, namespace isolation and cross-server orchestration. |
| Core Protocol & Agent Logic | Protocol Translation | Supports multiple transports such as stdio, Server-Sent Events and HTTP. | Evaluate automatic conversion across protocols for compatibility with different runtimes. |
| Core Protocol & Agent Logic | REST‑to‑MCP Wrapper | Ability to expose existing REST APIs as MCP tools. | Look for OpenAPI import, auth passthrough and seamless conversion. |
| Core Protocol & Agent Logic | Tool Discovery | Mechanism to introspect server capabilities and list tools, resources or schemas. | Check for API endpoints that enumerate tools and provide schema/parameters. |
| Core Protocol & Agent Logic | Session Management | Maintains stateful sessions between clients and servers for persistent interactions. | Assess session persistence, concurrency handling and ability to resume after failures. |
| Core Protocol & Agent Logic | Streaming Support | Provides real-time responses via streaming protocols like SSE or gRPC. | Check for backpressure handling and support for bidirectional streams. |
| Security & Compliance | Client Authentication | Mechanisms for verifying the identity of calling clients. | Verify support for OAuth 2.0, OIDC, API keys and mutual TLS. |
| Security & Compliance | Authorization/RBAC | Controls which agents can call which tools. | Look for per-tool permissions, role-based access control and team scopes. |
| Security & Compliance | Server Authentication | Verifies the identity of registered servers to prevent rogue services. | Evaluate server registration authentication and support for mTLS. |
| Security & Compliance | Sandboxing | Isolation of tool execution from the host environment to contain security risks. | Check for container, VM or WASM isolation, resource limits and egress filtering. |
| Security & Compliance | Secret Management | Secure storage and retrieval of credentials and API keys. | Assess integration with secret stores like Vault or cloud key managers and support for rotation. |
| Security & Compliance | Audit Logging | Capture immutable logs of requests and responses for compliance and forensics. | Look for full request/response capture, tamper-proof storage and queryability. |
| Security & Compliance | PII Redaction | Automatic removal or masking of personally identifiable information. | Check for regex-based and ML-based detection; support for structured and unstructured data. |
| Security & Compliance | Network Isolation | Prevents lateral movement and enforces zero-trust networking principles. | Assess egress filtering, network segmentation and zero-trust policies. |
| Security & Compliance | Threat Detection | Detects anomalies and attacks like prompt injection or tool poisoning. | Look for runtime anomaly detection and signature-based protections. |
| Security & Compliance | Compliance Mappings | Alignment with regulations such as GDPR, HIPAA, SOX or FedRAMP. | Check for certifications or attestations and features supporting compliance (data residency, encryption). |
| Performance & Scalability | Latency Overhead | Added latency introduced by the gateway; low overhead is critical for interactive agents. | Look for P50/P95/P99 latency metrics and optimization (e.g., in-memory caching). |
| Performance & Scalability | Throughput | Maximum number of requests per second each node can handle. | Evaluate horizontal scalability and concurrency limits. |
| Performance & Scalability | Session Capacity | Number of concurrent sessions that can be maintained. | Assess connection limits, memory footprint and session storage. |
| Performance & Scalability | High Availability | Gateway’s ability to remain operational despite failures. | Check for multi-zone deployment, automatic failover and SLO commitments. |
| Performance & Scalability | Resource Efficiency | Optimises CPU and memory usage to reduce cost. | Look at footprint, start-up time and overhead on underlying workloads. |
| Performance & Scalability | Auto‑scaling |  |  |
| Operations & Reliability | Observability | Ability to collect and export metrics, logs and traces. | Ensure OTEL export, integration with monitoring stacks and correlation of events. |
| Operations & Reliability | Health Checks | Probes to verify liveness and readiness for deployments. | Check for HTTP/gRPC health endpoints and Kubernetes probe configuration. |
| Operations & Reliability | Circuit Breakers | Mechanisms to prevent cascading failures and allow graceful recovery. | Look for automatic retries, backoff and failover logic. |
| Operations & Reliability | Configuration | Flexibility to change settings without downtime and support for GitOps. | Assess hot reload, declarative configuration and validation tools. |
| Operations & Reliability | Debugging Tools | Tools to trace and replay requests or inspect traffic. | Look for debug UIs, traffic inspection and request replay features. |
| Operations & Reliability | Alerting | Notifications when performance thresholds are breached or anomalies occur. | Evaluate threshold-based and anomaly detection alerts integrated with operations systems. |
| Operations & Reliability | Backup & Recovery | Procedures to back up registries and restore configurations. | Look for export/import capabilities, database snapshots and disaster recovery guides. |
| Operations & Reliability | Upgrade Strategy | Support for zero-downtime updates. | Check for rolling updates, blue-green or canary deployments. |
| Developer Experience | Admin UI | Graphical interface to manage servers and policies. | Evaluate usability, multi-tenancy support and role segregation. |
| Developer Experience | CLI Tools | Command-line utilities for automation. | Check for scripting support, bulk operations and integration with CI/CD. |
| Developer Experience | API Documentation | Clarity of APIs via OpenAPI specs, code examples and tutorials. | Look for comprehensive docs, sample code and interactive portals. |
| Developer Experience | SDK Support | Availability of client libraries for different languages. | Check languages supported and community contributions. |
| Developer Experience | Local Development | Ease of running gateways locally for testing. | Assess Docker Compose files, local emulators and dev guides. |
| Developer Experience | Server Templates | Pre-built templates and generators for new servers. | Look for boilerplate code, scaffolding tools and example servers. |
| Developer Experience | Testing Framework | Support for integration or unit testing of tools and policies. | Check for mocks, sandboxes and test harnesses. |
| Developer Experience | Migration Tools | Assistance in adopting the gateway and importing existing definitions. | Evaluate import/export from other gateways and data migration paths. |
| Architecture & Integration | Deployment Models | Options for running the gateway (SaaS, self-hosted, hybrid, air-gapped). | Ensure the model aligns with compliance and operational needs. |
| Architecture & Integration | Platform Support | Supported infrastructure environments (Kubernetes, Docker, VMs, serverless). | Check for official Helm charts, containers and serverless adapters. |
| Architecture & Integration | Cloud Providers | Ability to deploy on multiple cloud providers or on-premise. | Evaluate support for AWS, Azure, GCP and bare metal. |
| Architecture & Integration | IdP Integration | Integration with identity providers for SSO. | Check support for Okta, Azure AD, Auth0, Keycloak and SAML. |
| Architecture & Integration | Secrets Backend | Backend services for storing credentials securely. | Look for integration with Vault, AWS Secrets Manager, Azure Key Vault or GCP Secret Manager. |
| Architecture & Integration | Observability Stack | Out-of-the-box integration with monitoring tools (Prometheus, Datadog, Splunk). | Assess support for metrics exporters and log sinks. |
| Architecture & Integration | Service Mesh | Support for Istio, Linkerd or other service meshes. | Check for sidecar or native integration and policy enforcement. |
| Architecture & Integration | Policy Engine | External policy enforcement using OPA or similar engines. | Look for support to call out to OPA/Cedar for fine-grained policies. |
| Architecture & Integration | Plugin System | Mechanism for extending gateway functionality via plugins. | Check for WASM, Lua, Go or other plugin runtimes and extension points. |
| Architecture & Integration | API Compatibility | Integration with LLM gateways or AI platforms and compatibility with other API standards. | Assess support for open standards, ability to call external AI models or LLMs. |