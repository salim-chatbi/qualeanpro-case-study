<div align="center">

# QualeanPro

### Cloud-Native E-Learning Platform

**Public Engineering Case Study**

> The production source code is private and is not included in this repository.

<br>

![Java](https://img.shields.io/badge/Java-17%2F21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-19-DD0031?style=for-the-badge&logo=angular&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Production-2496ED?style=for-the-badge&logo=docker&logoColor=white)

![Kafka](https://img.shields.io/badge/Kafka-Event_Driven-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Data-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Keycloak](https://img.shields.io/badge/Keycloak-IAM-4D4D4D?style=flat-square)
![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-Observability-F46800?style=flat-square&logo=grafana&logoColor=white)

</div>

---

## Overview

QualeanPro is a **production-oriented e-learning platform** built around a modern **microservices architecture**.

It supports:

- training and course management;
- consultations;
- certificate workflows;
- user and profile management;
- online learning experiences;
- secure authentication and authorization;
- asynchronous communication;
- object storage;
- CI/CD;
- monitoring and production operations.

This repository is a **public engineering case study** focused on the architecture, technical decisions, infrastructure and production challenges behind the platform.

No private source code, credentials or sensitive production information is exposed.

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

### 🧭 Overview
- [Project Overview](#project-overview)
- [My Role](#my-role)
- [High-Level Architecture](#high-level-architecture)
- [System Components](#system-components)
- [Core Business Capabilities](#core-business-capabilities)

### 🔐 Architecture & Security
- [Identity & Access Management](#identity--access-management)
- [Network & Exposure Model](#network--exposure-model)
- [Data & Storage Strategy](#data--storage-strategy)
- [Event-Driven Communication](#event-driven-communication)
- [Service Discovery & Configuration](#service-discovery--configuration)
- [Containerized Architecture](#containerized-architecture)

</td>
<td valign="top" width="50%">

### 🚀 Production & Operations
- [Production Engineering](#production-engineering)
- [CI/CD Pipeline](#cicd-pipeline)
- [Observability & Health](#observability--health)
- [Backup & Recovery](#backup--recovery)
- [Real Engineering Challenges](#real-engineering-challenges)

### 🧠 Engineering & Evolution
- [Key Engineering Decisions](#key-engineering-decisions)
- [Engineering Principles](#engineering-principles)
- [Current Technical Evolution](#current-technical-evolution)
- [AI & RAG Exploration](#ai--rag-exploration)
- [Architecture Evolution](#architecture-evolution)
- [What This Project Demonstrates](#what-this-project-demonstrates)

### 📌 Project Details
- [Confidentiality](#confidentiality)
- [Project Information](#project-information)

</td>
</tr>
</table>

---

QualeanPro was designed to provide a scalable digital learning environment capable of supporting:

<table>
<tr>
<td>👤 User & profile management</td>
<td>🎓 Training & course management</td>
<td>💬 Consultation services</td>
</tr>
<tr>
<td>📜 Certificate generation</td>
<td>🎥 Zoom session integration</td>
<td>🔐 Authentication & authorization</td>
</tr>
<tr>
<td>⚡ Asynchronous communication</td>
<td>🗂️ Object storage</td>
<td>📊 Monitoring & observability</td>
</tr>
<tr>
<td>🔄 CI/CD automation</td>
<td>🚀 Production deployment</td>
<td>🛡️ Production reliability</td>
</tr>
</table>

Engineering Priorities

Scalability · Maintainability · Security · Observability · Cloud-Native Practices · Production Reliability

My Role

I contributed to the design, development and production deployment of the platform across multiple technical areas.

<table>
<tr>
<td valign="top" width="50%">

Backend Engineering

Java & Spring Boot microservices

REST API design

Service-to-service communication

Configuration management

Service discovery

API gateway integration

PostgreSQL persistence

Kafka asynchronous processing

Redis caching

</td>
<td valign="top" width="50%">

Frontend

Angular SPA integration

Authentication flow integration

API communication through the gateway

Production frontend deployment

Security

Keycloak-based IAM

OAuth2 / OpenID Connect

PKCE

Role-based access control

Secured application access

</td>
</tr>
<tr>
<td valign="top">

DevOps & Production

Docker & Docker Compose

GitHub Actions CI/CD

Nginx reverse proxy

HTTPS / TLS

Ubuntu production deployment

Container resource management

Persistent volume management

Backup strategy

Monitoring & troubleshooting

</td>
<td valign="top">

Observability

Prometheus

Grafana

Centralized logs

Service health checks

Production monitoring

</td>
</tr>
</table>

High-Level Architecture

                              Internet
                                 │
                                 ▼
                              Nginx
                                 │
                    ┌────────────┴────────────┐
                    │                         │
                    ▼                         ▼
             Angular Frontend            API Gateway
                                              │
                                              ▼
                                   Service Discovery
                                              │
               ┌──────────────────────────────┼──────────────────────────────┐
               │                              │                              │
               ▼                              ▼                              ▼
         User Service                 Formation Service           Consultation Service
               │                              │                              │
               │                              ▼                              │
               │                      Certificate Service                   │
               │                              │                              │
               └────────────────────── Services Service ────────────────────┘
                                              │
                         ┌────────────────────┼────────────────────┐
                         │                    │                    │
                         ▼                    ▼                    ▼
                    PostgreSQL             Redis                 Kafka
                                              │
                                              ▼
                                             MinIO

                                 Keycloak
                                    │
                                    └── Authentication / Authorization

Design goal: separate business and technical responsibilities while keeping services independently deployable, observable and easier to evolve.

System Components

Component

Responsibility

frontend

Angular single-page application

gateway-service

Central API entry point and request routing

service-registry

Service discovery

config-server

Centralized application configuration

user-service

User profiles and user-related operations

formation-service

Training and course management

consultation-service

Consultation workflows

certificat-service

Certificate generation and validation

services-service

Additional business services

Keycloak

Authentication and authorization

PostgreSQL

Relational persistence

Redis

Cache and ephemeral data

Kafka

Asynchronous event communication

MinIO

Object and file storage

Nginx

Reverse proxy and HTTPS entry point

Core Business Capabilities

<details open>
<summary><strong>🎓 Training Management</strong></summary>

courses and training programs;

training domains and categories;

trainer-related information;

course lifecycle management;

training assignment;

learning content.

</details>

<details>
<summary><strong>👤 User Management</strong></summary>

user profiles;

personal information;

authentication integration;

authorization;

profile-related documents and resources.

</details>

<details>
<summary><strong>💬 Consultation Services</strong></summary>

The platform supports different consultation offerings and service levels.

The consultation domain is isolated from training management to keep business responsibilities separated.

</details>

<details>
<summary><strong>📜 Certificate Management</strong></summary>

certificate generation;

certificate identifiers;

PDF certificates;

QR-based certificate verification;

certificate lifecycle management.

</details>

<details>
<summary><strong>🎥 Online Sessions</strong></summary>

The platform integrates remote learning sessions through Zoom:

session creation;

synchronization;

updates;

session deletion;

association with training activities.

</details>

Identity & Access Management

Authentication and authorization are delegated to Keycloak instead of being implemented directly inside the application.

Authentication Flow

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
 ├──────────────► User Service
 ├──────────────► Formation Service
 ├──────────────► Consultation Service
 ├──────────────► Certificate Service
 └──────────────► Services Service

Security Principles

Principle

Implementation

Centralized authentication

Keycloak

Standard identity protocols

OAuth2 / OpenID Connect

SPA protection

PKCE

Access token model

JWT

Authorization

Role-based access control

Public exposure

Nginx / HTTPS only where required

Internal services

Not directly exposed to the Internet

Network & Exposure Model

                        Internet
                           │
                     HTTPS / 443
                           │
                           ▼
                         Nginx
                           │
              ┌────────────┴────────────┐
              │                         │
          Frontend                 API Gateway
                                        │
                            Internal Docker Network
                                        │
       ┌────────────────────────────────┼─────────────────────────────┐
       │                                │                             │
 Microservices                      Keycloak                     Middleware
                                                                    │
                                         ┌──────────────────────────┼─────────────┐
                                         │                          │             │
                                    PostgreSQL                    Redis         Kafka
                                         │
                                       MinIO

PostgreSQL, Redis, Kafka and MinIO are not intended to be directly reachable from the public Internet.

Data & Storage Strategy

<table>
<tr>
<td width="25%" valign="top"><strong>PostgreSQL</strong><br><br>Transactional and relational application data.</td>
<td width="25%" valign="top"><strong>Redis</strong><br><br>Fast-access temporary data and caching where justified.</td>
<td width="25%" valign="top"><strong>Kafka</strong><br><br>Asynchronous event communication.</td>
<td width="25%" valign="top"><strong>MinIO</strong><br><br>Centralized object and file storage.</td>
</tr>
</table>

Object Storage Evolution

Old approach                          Target approach

Microservice                          Microservices
    │                                     │
    └── Local /uploads                    ▼
                                        MinIO
                                          │
                                          ├── user objects
                                          ├── training resources
                                          ├── certificates
                                          └── application files

This improves persistence, portability, backup management and separation between application runtime and file storage.

Event-Driven Communication

Producer Service
       │
       │ Event
       ▼
     Kafka
       │
       ├──────────► Consumer A
       │
       └──────────► Consumer B

Kafka is used where asynchronous communication provides architectural value and reduces tight coupling between services.

Service Discovery & Configuration

                     Config Server
                          │
              centralized configuration
                          │
                          ▼
                    Microservices


                    Service Registry
                          ▲
                          │ registration
           ┌──────────────┼───────────────┐
           │              │               │
       Service A      Service B       Service C

Containerized Architecture

Docker Host
│
├── nginx
├── frontend
├── gateway-service
├── service-registry
├── config-server
├── user-service
├── formation-service
├── consultation-service
├── certificat-service
├── services-service
├── keycloak
├── postgres
├── redis
├── kafka
└── minio

Containerization provides: consistent environments · reproducible deployments · service isolation · simplified dependency management · easier rollback · resource limits per service.

Production Engineering

Container Resource Management

Container Memory Limit
        │
        ├── JVM Heap
        ├── Metaspace
        ├── Native Memory
        ├── Thread Stacks
        └── Other JVM / OS allocations

Operational work includes:

monitoring container memory utilization;

checking Docker memory limits;

monitoring OOMKilled events;

tuning JVM memory settings;

adjusting service memory allocation when justified.

Persistent Volume Strategy

Stateful services include:

PostgreSQL · Keycloak · Redis · Kafka · MinIO

Production maintenance includes:

identifying anonymous Docker volumes;

replacing unclear volumes with explicit names;

migrating data safely;

documenting volume ownership;

maintaining rollback capability;

removing obsolete volumes only after verification.

Example target naming:

qualeanpro-prod_postgres_data
qualeanpro-prod_keycloak_data
qualeanpro-prod_redis_data
qualeanpro-prod_kafka_data
qualeanpro-prod_minio_data

CI/CD Pipeline

Developer
    │
    ▼
Git Push
    │
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ├── Build application
    ├── Run validation
    ├── Build Docker image
    ├── Tag image
    ├── Publish image
    └── Deploy
          │
          ▼
      Production

Production images are versioned using immutable identifiers instead of relying only on latest.

Git Commit
    │
    ▼
Docker Image Tag
    │
    ▼
Production Deployment

Reverse Proxy & HTTPS

Nginx acts as the public entry point.

Client
  │
  │ HTTPS
  ▼
Nginx
  │
  ├────────► Angular Frontend
  │
  └────────► API Gateway

Responsibilities include:

HTTPS termination · frontend delivery · API routing · security headers · reverse proxying · public/internal separation

Observability & Health

<table>
<tr>
<td width="33%" valign="top">

Metrics

Prometheus

CPU usage

Memory usage

Application metrics

Disk utilization

</td>
<td width="33%" valign="top">

Visualization

Grafana

Infrastructure status

Service health

Runtime visibility

</td>
<td width="33%" valign="top">

Health

Docker health checks

Service availability

Failure detection

Production diagnostics

</td>
</tr>
</table>

Container running
        ≠
Application ready

Backup & Recovery

Protected data domains:

PostgreSQL
    └── transactional data

MinIO
    └── object storage

Operational approach:

Scheduled Backups → Retention → Verification → Recovery Documentation → Disaster Recovery Planning

A backup is considered useful only if restoration has been considered as part of the process.

Production Operations

<details>
<summary><strong>View operational responsibilities</strong></summary>

Ubuntu server maintenance;

kernel updates;

controlled server reboots;

Docker health verification;

container resource auditing;

volume management;

backup verification;

log inspection;

HTTPS verification;

service availability checks;

deployment validation.

Maintenance Validation Flow

Backup verification
        │
        ▼
System maintenance
        │
        ▼
Server restart
        │
        ▼
Docker recovery
        │
        ▼
Service health checks
        │
        ▼
HTTPS verification
        │
        ▼
Application validation

</details>

Real Engineering Challenges

<details open>
<summary><strong>🌐 CORS Configuration</strong></summary>

Frontend and API communication required correctly aligning:

Browser → Angular → Nginx → Gateway → Backend services

Incorrect CORS configuration could block valid requests even when backend services were operational.

</details>

<details>
<summary><strong>🔐 Keycloak Redirect Configuration</strong></summary>

Authentication flows required correct redirect URI and client configuration.

Angular SPA
     │
     ▼
Keycloak Client
     │
     ▼
Configured Redirect URI

A typical issue was invalid_redirect_uri.

</details>

<details>
<summary><strong>🐳 Container DNS & Networking</strong></summary>

Errors such as UnknownHost required validating:

Docker network membership;

service names;

Compose configuration;

container health;

startup dependencies.

</details>

<details>
<summary><strong>🗄️ Database Availability</strong></summary>

Stateful services must be ready before dependent applications can operate correctly.

This required:

health checks;

retry strategies;

startup dependency management;

database diagnostics.

</details>

<details>
<summary><strong>🧠 Memory Pressure</strong></summary>

Host RAM
      vs
Container RAM Limit
      vs
JVM Heap

Java microservices can approach Docker memory limits even when the host still has available RAM.

</details>

<details>
<summary><strong>💾 Persistent Storage Migration</strong></summary>

Identify
   ↓
Backup
   ↓
Create named volume / target storage
   ↓
Copy data
   ↓
Validate
   ↓
Switch service
   ↓
Monitor
   ↓
Retain rollback
   ↓
Remove legacy storage

</details>

Key Engineering Decisions

Decision

Rationale

Microservices

Isolate major business capabilities and allow independent evolution

Keycloak

Rely on standard IAM protocols instead of implementing authentication manually

Kafka

Use asynchronous communication where decoupling provides value

Redis

Use fast temporary/cache storage selectively

MinIO

Keep object storage independent from disposable application containers

Docker

Reproducible environments, isolation and operational consistency

Engineering Principles

<div align="center">

Separation of Concerns · Disposable Application Containers · Persistent State Outside Runtime

Secure-by-Default Exposure · Automation Before Manual Deployment

Observability by Design · Production Operations as Software Engineering

</div>

Current Technical Evolution

The following items represent the evolution roadmap and should not be interpreted as all being currently available in production.

improved learning progression tracking;

video progress validation;

final quizzes;

payment workflows;

trainer commission management;

enterprise training packages;

AI-assisted orientation;

AI-assisted CV services;

trainer application workflows;

improved refund workflows;

Kubernetes deployment;

Infrastructure as Code;

stronger DevSecOps practices;

advanced observability;

disaster-recovery automation;

Retrieval-Augmented Generation.

AI & RAG Exploration

Platform Knowledge
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
Context-Grounded Response

Technologies being explored:






Architecture Evolution

<table>
<tr>
<td width="50%" valign="top">

Current

Ubuntu Server
    │
Docker Compose
    │
Microservices

</td>
<td width="50%" valign="top">

Target Evolution

Infrastructure as Code
        │
        ▼
Cloud Infrastructure
        │
        ▼
Kubernetes
        │
        ▼
Microservices
        │
        ├── Autoscaling
        ├── Service Discovery
        ├── Secrets Management
        ├── Centralized Observability
        └── Automated Recovery

</td>
</tr>
</table>

Kubernetes is considered when operational requirements justify orchestration—not simply to add complexity.

What This Project Demonstrates

Requirements
    │
    ▼
Architecture
    │
    ▼
Development
    │
    ▼
Security
    │
    ▼
Testing
    │
    ▼
Containerization
    │
    ▼
CI/CD
    │
    ▼
Deployment
    │
    ▼
Monitoring
    │
    ▼
Production Operations
    │
    ▼
Continuous Improvement

QualeanPro demonstrates experience not only in building application features, but also in making software deployable, observable, maintainable and operable in production.

Case Study Repository

qualeanpro-case-study/
├── README.md
│
├── docs/
│   ├── architecture.md
│   ├── security.md
│   ├── deployment.md
│   ├── ci-cd.md
│   ├── observability.md
│   └── engineering-decisions.md
│
├── diagrams/
│   ├── system-context.png
│   ├── microservices-architecture.png
│   ├── authentication-flow.png
│   └── deployment-architecture.png
│
└── screenshots/
    └── anonymized-public-screenshots/

Confidentiality

[!IMPORTANT]
QualeanPro is a private project. The production source code is intentionally not published in this repository.

This public case study does not expose:

proprietary source code;

credentials or API secrets;

private keys;

production environment variables;

internal infrastructure addresses;

database dumps;

customer or user data;

sensitive business information;

confidential operational configuration.

Only architecture concepts and non-sensitive engineering information are presented.

Project Information

Information

Value

Project

QualeanPro

Domain

E-Learning

Architecture

Microservices

Backend

Java / Spring Boot

Frontend

Angular

Database

PostgreSQL

Messaging

Kafka

Cache

Redis

IAM

Keycloak

Object Storage

MinIO

Containers

Docker

Reverse Proxy

Nginx

CI/CD

GitHub Actions

Monitoring

Prometheus / Grafana

Environment

Ubuntu

Source Code

Private

Case Study

Public

Status

Active

Engineering Areas Demonstrated

<div align="center">








Distributed Systems · REST APIs · Redis · Keycloak · OAuth2 · OpenID Connect · PKCE
MinIO · Docker Compose · GitHub Actions · Nginx · Linux · Prometheus · Grafana
CI/CD · DevOps · Cloud-Native · Production Operations

</div>

<div align="center">

Building software is only the beginning.

Reliable software must also be secured, deployed, monitored, maintained and continuously improved.

</div>
