<div align="center">

# QualeanPro

### Cloud-Native E-Learning Platform

**Public Engineering Case Study**

> The production source code is private and is not included in this repository.

<br>

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-19-DD0031?style=for-the-badge&logo=angular&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Production-2496ED?style=for-the-badge&logo=docker&logoColor=white)

![Kafka](https://img.shields.io/badge/Kafka-Event_Driven-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Data-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Keycloak](https://img.shields.io/badge/Keycloak-IAM-4D4D4D?style=flat-square)
![Redis](https://img.shields.io/badge/Redis-Cache-DC382D?style=flat-square&logo=redis&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-Observability-F46800?style=flat-square&logo=grafana&logoColor=white)

</div>

---

## Overview

QualeanPro is a **production-oriented e-learning platform** built around a modern **microservices architecture**.

It combines application development, distributed systems, security, DevOps and production operations to support:

- training and course management;
- consultations;
- certification workflows;
- user and profile management;
- online sessions;
- secure authentication and authorization;
- asynchronous communication;
- object storage;
- CI/CD;
- observability and production monitoring.

This public repository presents the **engineering architecture, technical decisions and production challenges** behind the platform without exposing private source code or sensitive infrastructure information.

<br>

<table>
<tr>
<td align="center" width="25%">

### 🏗️ Architecture
**Microservices**

</td>
<td align="center" width="25%">

### ☕ Backend
**Java / Spring Boot**

</td>
<td align="center" width="25%">

### 🌐 Frontend
**Angular**

</td>
<td align="center" width="25%">

### 🐳 Runtime
**Docker / Ubuntu**

</td>
</tr>

<tr>
<td align="center">

### ⚡ Messaging
**Kafka**

</td>
<td align="center">

### 🗄️ Data
**PostgreSQL / Redis**

</td>
<td align="center">

### 🔐 Security
**Keycloak / OIDC / PKCE**

</td>
<td align="center">

### 📊 Observability
**Prometheus / Grafana**

</td>
</tr>
</table>

---

## 📚 Table of Contents

<table>
<tr>
<td valign="top" width="50%">

### 🧭 Architecture
- [Project Overview](#project-overview)
- [My Role](#my-role)
- [High-Level Architecture](#high-level-architecture)
- [System Components](#system-components)
- [Identity & Security](#identity--security)

</td>
<td valign="top" width="50%">

### 🚀 Engineering
- [Production Engineering](#production-engineering)
- [CI/CD & Observability](#cicd--observability)
- [Engineering Challenges](#engineering-challenges)
- [Key Decisions](#key-decisions)
- [Evolution](#evolution)

</td>
</tr>
</table>

---

## 🎯 Project Overview

QualeanPro was designed to provide a **scalable digital learning environment** covering both business capabilities and production-grade technical concerns.

<table>
<tr>
<td align="center" width="33%">

### 👤 User Management
Profiles, identity-related data and user operations

</td>
<td align="center" width="33%">

### 🎓 Training Management
Courses, programs and learning content

</td>
<td align="center" width="33%">

### 💬 Consultations
Structured consultation workflows

</td>
</tr>

<tr>
<td align="center">

### 📜 Certification
PDF certificates and validation workflows

</td>
<td align="center">

### 🎥 Online Sessions
Zoom session integration and synchronization

</td>
<td align="center">

### 🔐 Security
Authentication, authorization and access control

</td>
</tr>

<tr>
<td align="center">

### ⚡ Event Processing
Asynchronous communication with Kafka

</td>
<td align="center">

### 🗂️ Object Storage
Centralized storage with MinIO

</td>
<td align="center">

### 📊 Operations
CI/CD, monitoring and production reliability

</td>
</tr>
</table>

### ⚙️ Engineering Priorities

<div align="center">

`Scalability` · `Maintainability` · `Security` · `Observability` · `Cloud-Native Practices` · `Reliability`

</div>

---

## 👨‍💻 My Role

I contributed to the **design, development and production deployment** of QualeanPro across multiple engineering areas.

<table>
<tr>
<td valign="top" width="50%">

### ☕ Backend Engineering

- Java & Spring Boot microservices
- REST API design
- Service-to-service communication
- Service discovery
- Centralized configuration
- API Gateway integration
- PostgreSQL persistence
- Kafka asynchronous processing
- Redis caching

</td>
<td valign="top" width="50%">

### 🌐 Frontend & Security

**Frontend**
- Angular SPA integration
- Authentication flow integration
- Gateway-based API communication
- Production frontend deployment

**Security**
- Keycloak-based IAM
- OAuth2 / OpenID Connect
- PKCE
- Role-based access control

</td>
</tr>

<tr>
<td valign="top">

### 🚀 DevOps & Production

- Docker & Docker Compose
- GitHub Actions CI/CD
- Nginx reverse proxy
- HTTPS / TLS
- Ubuntu production deployment
- Resource management
- Persistent volumes
- Backup strategy

</td>
<td valign="top">

### 📊 Observability

- Prometheus
- Grafana
- Centralized logging
- Docker health checks
- Service availability monitoring
- Production diagnostics

</td>
</tr>
</table>

---

## 🏗️ High-Level Architecture

QualeanPro follows a layered microservices architecture with a **single public entry point, centralized IAM, dedicated platform services and isolated business services**.

```text
┌──────────────────────────────────────────────────────────────────────────────┐
│                                CLIENT LAYER                                  │
│                                                                              │
│                         Web Browser / End User                               │
└──────────────────────────────────────┬───────────────────────────────────────┘
                                       │ HTTPS
                                       ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                              EDGE / ENTRY LAYER                              │
│                                                                              │
│                         Nginx — Reverse Proxy + TLS                          │
└───────────────────────┬───────────────────────────────┬──────────────────────┘
                        │                               │
                        ▼                               ▼
              ┌──────────────────┐            ┌──────────────────┐
              │ Angular Frontend │            │   API Gateway    │
              │       SPA        │            │ Central API Edge │
              └─────────┬────────┘            └─────────┬────────┘
                        │                               │
                        │ OIDC / PKCE                   │ JWT / Routing
                        ▼                               ▼
              ┌──────────────────┐
              │     Keycloak     │
              │ Identity & Access│
              │    Management    │
              └──────────────────┘

┌──────────────────────────────────────────────────────────────────────────────┐
│                         PLATFORM SERVICES LAYER                              │
│                                                                              │
│        ┌──────────────────────┐       ┌──────────────────────┐               │
│        │   Service Registry   │       │    Config Server     │               │
│        │ Service Discovery    │       │ Centralized Config   │               │
│        └──────────────────────┘       └──────────────────────┘               │
└──────────────────────────────────────────────────────────────────────────────┘
                                       │
                                       ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                         BUSINESS SERVICES LAYER                              │
│                                                                              │
│   ┌───────────────┐   ┌──────────────────┐   ┌──────────────────────┐       │
│   │ User Service  │   │ Formation Service│   │ Consultation Service │       │
│   └───────────────┘   └────────┬─────────┘   └──────────────────────┘       │
│                                │                                             │
│                       ┌────────▼──────────┐                                  │
│                       │Certificate Service│                                  │
│                       └────────┬──────────┘                                  │
│                                │                                             │
│                       ┌────────▼────────┐                                    │
│                       │Services Service │                                    │
│                       └─────────────────┘                                    │
└──────────────────────────────────────────────────────────────────────────────┘
                                       │
                ┌──────────────────────┼──────────────────────┐
                │                     │                      │
                ▼                     ▼                      ▼
       ┌────────────────┐    ┌────────────────┐     ┌────────────────┐
       │   PostgreSQL   │    │     Redis      │     │     Kafka      │
       │ Relational Data│    │ Cache/Ephemeral│     │ Event Streaming│
       └────────────────┘    └────────────────┘     └────────────────┘

                         ┌─────────────────────────┐
                         │          MinIO          │
                         │ Object & Document Store │
                         └─────────────────────────┘
```

> [!NOTE]
> **Architecture Principle:** Separate edge, identity, platform services, business domains, persistence, messaging and object storage to improve **maintainability, scalability, security and independent service evolution**.

---

## 🧩 System Components

| Component | Responsibility |
|---|---|
| `frontend` | Angular single-page application |
| `gateway-service` | API entry point and request routing |
| `service-registry` | Service discovery |
| `config-server` | Centralized configuration |
| `user-service` | User profiles and related operations |
| `formation-service` | Training and course management |
| `consultation-service` | Consultation workflows |
| `certificat-service` | Certificate generation and validation |
| `services-service` | Additional business services |
| `Keycloak` | Identity and access management |
| `PostgreSQL` | Relational persistence |
| `Redis` | Cache and ephemeral data |
| `Kafka` | Asynchronous event communication |
| `MinIO` | Object and document storage |
| `Nginx` | Reverse proxy and HTTPS entry point |

---

## 🔐 Identity & Security

Authentication and authorization are delegated to **Keycloak** using industry-standard identity protocols.

```text
User
 │
 ▼
Angular SPA
 │
 │ OAuth2 / OIDC + PKCE
 ▼
Keycloak
 │
 │ Access Token
 ▼
API Gateway
 │
 ├──► User Service
 ├──► Formation Service
 ├──► Consultation Service
 ├──► Certificate Service
 └──► Services Service
```

| Security Concern | Implementation |
|---|---|
| Authentication | Keycloak |
| Identity Protocols | OAuth2 / OpenID Connect |
| SPA Protection | PKCE |
| Token Model | JWT |
| Authorization | RBAC |
| Public Entry Point | Nginx / HTTPS |
| Internal Services | Not directly exposed publicly |

---

## 📦 Data & Communication

<table>
<tr>
<td width="25%" valign="top">

### PostgreSQL
Transactional and relational application data.

</td>
<td width="25%" valign="top">

### Redis
Caching and fast temporary data access.

</td>
<td width="25%" valign="top">

### Kafka
Asynchronous event-driven communication.

</td>
<td width="25%" valign="top">

### MinIO
Centralized object and document storage.

</td>
</tr>
</table>

### Event-Driven Communication

```text
Producer Service
       │
       │ Event
       ▼
     Kafka
       │
       ├──────────► Consumer A
       └──────────► Consumer B
```

Kafka is introduced where asynchronous communication improves **decoupling and scalability**, rather than replacing synchronous APIs everywhere.

---

## 🐳 Production Engineering

The platform currently runs as a **containerized production workload on Ubuntu**.

```text
Ubuntu Server
│
├── Nginx
├── Angular Frontend
├── API Gateway
├── Service Registry
├── Config Server
├── Business Microservices
├── Keycloak
├── PostgreSQL
├── Redis
├── Kafka
└── MinIO
```

### Operational Concerns

`Container Health` · `JVM Memory` · `Persistent Volumes` · `Backups` · `HTTPS` · `Logs` · `Service Availability`

### Persistent Storage

Stateful services use explicit Docker persistence.

```text
PostgreSQL
Keycloak
Redis
Kafka
MinIO
```

Operational work includes:

- volume identification and standardization;
- safe data migration;
- backup verification;
- resource monitoring;
- rollback planning.

---

## 🔄 CI/CD & Observability

<table>
<tr>
<td valign="top" width="50%">

### 🚀 CI/CD

```text
Git Push
   │
   ▼
GitHub Actions
   │
   ├── Build
   ├── Validate
   ├── Build Docker Image
   ├── Tag Image
   ├── Publish
   └── Deploy
          │
          ▼
      Production
```

Production Docker images are associated with immutable source revisions for better traceability.

</td>
<td valign="top" width="50%">

### 📊 Observability

**Prometheus**
- metrics collection;
- infrastructure monitoring;
- application metrics.

**Grafana**
- visualization;
- runtime visibility;
- infrastructure dashboards.

**Health Checks**
- container health;
- service availability;
- failure detection.

</td>
</tr>
</table>

> **Operational principle:** `Container running` does not necessarily mean `Application ready`.

---

## 🧯 Engineering Challenges

<details open>
<summary><strong>🌐 CORS & API Integration</strong></summary>

Frontend/backend communication required correctly aligning:

`Browser → Angular → Nginx → API Gateway → Microservices`

</details>

<details>
<summary><strong>🔐 Keycloak Authentication</strong></summary>

Authentication flows required correct OIDC client configuration, redirect URIs and SPA integration.

A representative issue was:

```text
invalid_redirect_uri
```

</details>

<details>
<summary><strong>🐳 Docker Networking</strong></summary>

Container communication issues such as `UnknownHost` required validating:

- Docker network membership;
- service names;
- Compose configuration;
- startup dependencies;
- container health.

</details>

<details>
<summary><strong>🧠 JVM & Container Memory</strong></summary>

```text
Host RAM
   ≠
Container Memory Limit
   ≠
JVM Heap
```

Production operation requires monitoring both the host and individual Java container limits.

</details>

<details>
<summary><strong>💾 Persistent Storage</strong></summary>

Legacy and anonymous Docker volumes require controlled migration:

```text
Identify → Backup → Migrate → Validate → Switch → Monitor → Remove Legacy Storage
```

</details>

---

## 🧠 Key Decisions

| Decision | Engineering Rationale |
|---|---|
| **Microservices** | Isolate business capabilities and support independent evolution |
| **Keycloak** | Use standardized IAM instead of implementing authentication manually |
| **Kafka** | Introduce asynchronous communication where decoupling provides value |
| **Redis** | Use fast cache/ephemeral storage selectively |
| **MinIO** | Separate object storage from disposable application containers |
| **Docker** | Reproducible environments and operational consistency |
| **GitHub Actions** | Automate build, packaging and deployment workflows |
| **Prometheus / Grafana** | Integrate observability into production operations |

---

## 📐 Engineering Principles

<div align="center">

`Separation of Concerns` · `Secure-by-Default`

`Disposable Application Containers` · `Persistent State Outside Runtime`

`Automation Before Manual Deployment` · `Observability by Design`

`Production Operations as Part of Software Engineering`

</div>

---

## 📈 Evolution

QualeanPro continues to evolve toward:

- advanced learning progression;
- quizzes and payment workflows;
- enterprise training packages;
- AI-assisted features;
- RAG capabilities;
- stronger DevSecOps practices;
- Infrastructure as Code;
- Kubernetes-based orchestration;
- improved disaster recovery and observability.

### AI / RAG Exploration

```text
Knowledge
   │
   ▼
Document Processing
   │
   ▼
Chunking
   │
   ▼
Embeddings
   │
   ▼
Vector Store
   │
   ▼
Retriever
   │
   ▼
LLM
   │
   ▼
Grounded Response
```

Technologies explored:

`Spring AI` · `LangChain4j` · `Ollama` · `PostgreSQL / pgvector`

---

## 🎓 What This Project Demonstrates

<div align="center">

**Requirements**

↓

**Architecture**

↓

**Development & Security**

↓

**Containerization & CI/CD**

↓

**Deployment & Observability**

↓

**Production Operations**

↓

**Continuous Improvement**

</div>

QualeanPro demonstrates experience beyond feature development: building software that is **deployable, secure, observable, maintainable and operable in production**.

---

## 🔒 Confidentiality

> [!IMPORTANT]
> QualeanPro is a private project. The production source code is intentionally **not published** in this repository.

This public case study does **not** expose:

- proprietary source code;
- credentials or API secrets;
- private keys;
- production environment variables;
- internal infrastructure addresses;
- database dumps;
- customer or user data;
- confidential operational configuration.

Only **non-sensitive architecture and engineering information** is presented.

---

## 📌 Project Information

| | |
|---|---|
| **Domain** | E-Learning |
| **Architecture** | Microservices |
| **Backend** | Java / Spring Boot |
| **Frontend** | Angular |
| **Database** | PostgreSQL |
| **Messaging** | Kafka |
| **Cache** | Redis |
| **IAM** | Keycloak |
| **Object Storage** | MinIO |
| **Containers** | Docker |
| **Reverse Proxy** | Nginx |
| **CI/CD** | GitHub Actions |
| **Observability** | Prometheus / Grafana |
| **Runtime** | Ubuntu |
| **Source Code** | Private |
| **Case Study** | Public |
| **Status** | Active |

---

<div align="center">

### Engineering Areas

![Java](https://img.shields.io/badge/Java-Backend-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-Microservices-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-SPA-DD0031?style=flat-square&logo=angular&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-Event_Driven-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?style=flat-square&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Data-4169E1?style=flat-square&logo=postgresql&logoColor=white)

<br>

`Distributed Systems` · `REST APIs` · `OAuth2` · `OIDC` · `PKCE` · `Redis` · `MinIO`  
`GitHub Actions` · `Nginx` · `Linux` · `Prometheus` · `Grafana` · `DevOps`

<br>

### Building software is only the beginning.

**Reliable software must also be secured, deployed, monitored, maintained and continuously improved.**

</div>
