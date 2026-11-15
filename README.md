# POS System Design: from monolith to cloud-native and AI

One point-of-sale (POS) product, designed five times, each time bigger: a single-store desktop app, then a multi-tenant, omnichannel, cloud-native microservices platform on Azure with an AI customer-support copilot.

**117 diagrams in one draw.io file.** You can read them version by version, or open any page on its own.

> 📂 **File:** [`POS System.drawio`](POS%20System.drawio)
> 🖥️ **Open with:** [app.diagrams.net](https://app.diagrams.net) (File → Open from → Device), the draw.io desktop app, or the VS Code *Draw.io Integration* extension.
> 🗂️ **Pages:** use the page tabs at the bottom of draw.io to move between diagrams.

---

## Why this repo
Most system design examples stop at "add a load balancer". This one shows what actually changes as a product grows:
- **More stores:** offline-first tills and sync.
- **More customers:** multi-tenancy, sharding, CDC, caching.
- **More channels:** payment gateways, DoorDash, Uber Eats, web shop.
- **More scale:** microservices, four deployment models, observability.
- **AI:** agents, RAG, MCP, guardrails.

---

## The five versions

| # | Version | What changes | Pages |
|---|---|---|---|
| v1 | **Monolith** | C# desktop POS on every till, MySQL per store, semi-integrated card terminal, split-payment sale, loyalty | 4 |
| v2 | **Multi-store, offline-first** | Store App with local SQLite + cloud sync, back office, procure-to-pay, stock transfers | 7 |
| v3 | **Multi-tenant SaaS** | C4 levels 1–4, tenant sharding, monthly partitions, read replicas, Redis, CDC (Debezium → Event Hubs), Elasticsearch, Blob + CDN, DNS | 19 |
| v4 | **Omnichannel** | Multiple payment gateways with routing and failover, DoorDash & Uber Eats, each store's own web shop | 12 |
| v5 | **Cloud-native microservices** | 25 services on Azure, REST / GraphQL / gRPC, Angular + Electron + Android + iOS, Docker & AKS, Azure DevOps, four tenancy models, HR & payroll | 20 |

## Deep-dive collections (v5)

| Collection | Pages | Highlights |
|---|---|---|
| **API design** | 13 | API catalogue, REST endpoints, GraphQL supergraph, gRPC contracts, security & gateway policies, events & webhooks, lifecycle & versioning, WebSockets, webhooks, Web PubSub, AMQP, Azure Service Bus |
| **BPMN 2.0** | 14 | POS sale, online order, procure-to-pay, attendance & leave, payroll run, tenant onboarding, returns & refunds, vendor payment (full / partial / advance), stock transfer, stock reconciliation, shift & cash, price & promotion, purchase return, end-of-day close |
| **Domain-Driven Design** | 7 | Subdomains, context map, aggregates (commerce, inventory, payroll), ubiquitous language, hexagonal service anatomy |
| **Event-Driven Architecture** | 6 | Event flow map, EventStorming, choreography saga, orchestration saga, CQRS & event sourcing, messaging reliability (outbox, inbox, DLQ, replay) |
| **AI customer support** | 15 | C4 context & container, agent + sub-agent architecture, Azure deployment, RAG pipeline, prompt & context engineering, MCP tools, guardrails, OWASP LLM Top 10, fallback / retry / circuit breaker, observability & evaluation, harvesting & self-learning, conversation flow, BPMN, ERD |

**Total: 4 + 7 + 19 + 12 + 20 + 13 + 14 + 7 + 6 + 15 = 117 pages.**

---

## Page guide

<details>
<summary><b>v1 – Monolith (4)</b></summary>

`POS-Monolith` · `Sales-01-Monolith` · `Sales-02-Monolith` · `ERD-Monolith`
</details>

<details>
<summary><b>v2 – Multi-store, offline-first (7)</b></summary>

`POS-Web` · `Web-Flow-01` (offline-first sale) · `Web-Flow-02` (sync) · `Web-Flow-03` (procure-to-pay & transfer) · `Web-ERD-01` · `Web-ERD-02` · `Web-ERD-03`
</details>

<details>
<summary><b>v3 – Multi-tenant SaaS (19)</b></summary>

**C4 & scaling:** `C4-Context` · `C4-Containers` · `C4-Container-02` · `C4-Component-01` (Core API) · `C4-Component-02` (Sync API) · `C4-Component-03` (CDC pipeline) · `C4-Code` · `C4-Deployment` · `C4-Deployment-Azure` · `Data-Tier-Scaling`
**Workflows:** `Workflow-Tenant Onboarding` · `Workflow-Request-Routing` · `Workflow-SalesAndSync` · `Workflow-Catalog` · `Workflow-Shard Rebalancing`
**ERDs:** `ERD Catalog` · `ERD-Organisation` · `ERD Sales` · `ERD Purchase`
</details>

<details>
<summary><b>v4 – Omnichannel (12)</b></summary>

`C4-Context-03` · `C4-Container-03` · `C4-Components-Payment` · `C4-Components-Marketplace` · `Workflow-Multi-Payment` · `C4-Marketplace-Order` · `Workflow-Menu & Availability` · `Workflow-Online-Order` · `ERD-Order` · `ERD-Payment` · `ERD Marketplace` · `Azure Deployment`
</details>

<details>
<summary><b>v5 – Cloud-native microservices (20)</b></summary>

**Architecture:** `C4-Content-Cloud-Native` · `C4-Container-Cloud-Native` · `Data Ownership - Cloud-Native` · `API Communication - Cloud-Native` · `C4-Component Attendance` · `C4-Component Payroll` · `C4-Payroll Engine`
**Tenancy & deployment:** `Tenancy Models` · `Deploy Multi-Tenant` · `Deploy Single-Tenant` · `Deploy On-Premise` · `Deploy Hybrid`
**Operations:** `Production Monitoring` · `Production Incident Flow` · `Azure DevOps CI/CD`
**HR & payroll:** `Workflow Attendance` · `Workflow Attendance Regularization` · `Workflow Payroll Run` · `ERD-Employee Leave` · `ERD Payroll`
</details>

<details>
<summary><b>API design (13)</b></summary>

`API Design - Product Catalog` · `API Design - REST` · `API Design - GraphQL` · `API Design - gRPC` · `API Design Security & Gateway` · `API Design Events & Webhook` · `API Design - Lifecycle & Versioning` · `Real-time & messaging` · `API Design WebSockets` · `API Design Webhook` · `API Design PubSub` · `API Design - AMQP` · `API Design Azure Bus`
</details>

<details>
<summary><b>BPMN 2.0 (14)</b></summary>

`BPMN - POS Sale` · `BPMN - Online Order` · `BPMN - Procure-to-pay` · `BPMN - Attendance & Leave Approval` · `BPMN - Payroll Run` · `BPMN - Tenant Onboarding` · `BPMN - Return & Refunds` · `BPMN - Vendor Payment` · `BPMN - Stock Transfer` · `BPMN Stock Reconciliation` · `BPMN - Shift & Cash Management` · `BPMN - Price & Promotion` · `BPMN - Purchase Return` · `BPMN - End-of-day`
</details>

<details>
<summary><b>Domain-Driven Design (7)</b></summary>

`DDD Subdomains` · `DDD Context Map` · `DDD Aggregates` · `DDD Inventory` · `DDD Payroll` · `DDD Ubiquitous` · `DDD Service Anatomy`
</details>

<details>
<summary><b>Event-Driven Architecture (6)</b></summary>

`EDA-01` event flow map · `EDA-02` EventStorming (sale to cash) · `EDA-03` choreography saga (online order) · `EDA-04` orchestration saga (vendor payment run) · `EDA-05` CQRS & event sourcing · `EDA-06` messaging reliability patterns
</details>

<details>
<summary><b>AI customer support – Support Copilot (15)</b></summary>

`AI Context` · `AI Container` · `AI Agent Architecture` · `AI Deployment` · `AI RAG Pipeline` · `AI Prompt & Context Enginnering` · `AI MCP Tools` · `AI Guardrails` · `AI OWASP` · `AI Resilience` · `AI Observability` · `AI Harvesting & self-learning` · `AI Support Conversation Flow` · `BPM AI-Assisted Support Case` · `AI ERD`
</details>

---

## Tech and concepts covered
**Architecture:** monolith → modular monolith → microservices · C4 model · DDD (bounded contexts, aggregates, context map, hexagonal) · event-driven architecture (sagas, CQRS, event sourcing, outbox / inbox) · BPMN 2.0

**APIs & messaging:** REST (OpenAPI) · GraphQL (federated supergraph, BFFs) · gRPC · WebSockets (Azure Web PubSub / SignalR) · webhooks (HMAC, retries, replay) · AMQP 1.0 (Azure Service Bus, Event Hubs) · AMQP 0-9-1 (RabbitMQ) · MQTT (IoT Hub) · CloudEvents · AsyncAPI

**Data:** MySQL (sharding by tenant, monthly partitions, read replicas) · Cosmos DB · Redis · Elasticsearch · CDC with Debezium · Blob + CDN · Microsoft Fabric

**Azure & DevOps:** Front Door · API Management · Application Gateway for Containers · AKS · Functions · Logic Apps · Service Bus · Event Hubs · IoT Hub · Key Vault · Azure Arc · Azure DevOps (CI/CD, GitOps, release rings) · Azure Monitor / App Insights / Grafana · Sentinel

**Clients:** Angular · Electron · Android · iOS · offline-first SQLite sync

**Domain:** split payments (cash / card / UPI / points) · loyalty tiers · multiple payment gateways with failover · DoorDash & Uber Eats · click & collect / delivery · procure-to-pay with 3-way match · vendor payments (full / partial / advance) · stock transfer & reconciliation · shift & cash · end-of-day · attendance (8 capture methods) · payroll with statutory rules

**AI:** LLM · RAG · vector database · agents & sub-agents · MCP · prompt & context engineering · guardrails · OWASP Top 10 for LLM apps · fallback / retry / circuit breaker · evaluation · harvesting & self-learning with human review

**Deployment models:** multi-tenant · single-tenant · on-premise · hybrid

---

## How to use it
- **Learning system design:** go v1 → v5 in order. Each version answers "what breaks next, and how do we fix it?"
- **Interview prep:** the DDD, EDA, API design and AI pages map to common senior and architect questions.
- **Starting a real project:** copy a page into your own draw.io file and change the names. Numbers on the diagrams (limits, timeouts, SLOs) are **example values**; confirm your own.

## Notes
- **Example names only:** gateway, cloud-region and model names are examples. Every icon is a generic shape, not a vendor logo.
- **Placeholder domain:** `yourpos.com` stands in for your real domain.
- **Theme:** the diagrams are drawn for draw.io's dark theme and also work in light mode.

## Contributing
Found a mistake or have an idea? Open an issue or a pull request. If this helped you, please ⭐ the repo so others can find it.

## License
Free to use for learning and for your own projects. A credit link back to this repo is appreciated.
