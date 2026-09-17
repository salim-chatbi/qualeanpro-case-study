QualeanPro — Cloud-Native E-Learning Platform

Public Engineering Case Study
The production source code is private and is not included in this repository.

QualeanPro is a production-oriented e-learning platform designed to support training management, consultations, certification workflows, user management and online learning experiences through a modern microservices architecture.

This repository presents the engineering decisions, architecture, infrastructure and technical challenges behind the platform without exposing private source code or sensitive production information.

🎯 Project Overview

QualeanPro was designed to provide a scalable digital learning environment capable of supporting:

user and profile management;

training and course management;

consultation services;

certificate generation;

Zoom session integration;

authentication and authorization;

asynchronous communication;

object storage;

monitoring and observability;

CI/CD automation;

production deployment.

The platform is built with a strong focus on:

scalability;

maintainability;

security;

observability;

cloud-native practices;

production reliability.

👨‍💻 My Role

I contributed to the design, development and production deployment of the platform across multiple technical areas.

Backend Engineering

Java and Spring Boot microservices

REST API design

service-to-service communication

configuration management

service discovery

API gateway integration

persistence with PostgreSQL

asynchronous processing with Kafka

caching with Redis

Frontend

Angular SPA integration

authentication flow integration

API communication through the gateway

production frontend deployment

Security

Keycloak-based Identity and Access Management

OAuth2

OpenID Connect

PKCE

role-based access control

secured application access

DevOps & Production

Docker and Docker Compose

GitHub Actions CI/CD

Nginx reverse proxy

HTTPS/TLS

production deployment on Ubuntu

container resource management

persistent volume management

backup strategy

monitoring and troubleshooting

Observability

Prometheus

Grafana

centralized logs

service health checks

production monitoring

🏗️ High-Level Architecture

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

🧩 System Components

QualeanPro is composed of several independently deployable services, each responsible for a specific business capability.

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

The architecture separates technical and business responsibilities while keeping each service independently deployable and observable.

🎯 Core Business Capabilities

Training Management

The training domain manages:

courses and training programs;

training domains and categories;

trainer-related information;

course lifecycle management;

training assignment;

learning content.

User Management

The user domain manages:

user profiles;

personal information;

authentication integration;

authorization;

profile-related documents and resources.

Consultation Services

The platform supports different consultation offerings and service levels.

The consultation domain is isolated from training management to keep business responsibilities separated.

Certificate Management

The certificate service is responsible for:

generating certificates;

assigning certificate identifiers;

producing PDF certificates;

QR-based certificate verification;

certificate lifecycle management.

Online Sessions

The platform integrates remote learning sessions through Zoom.

Supported technical workflows include:

session creation;

synchronization;

updates;

session deletion;

association with training activities.

🔐 Identity & Access Management

Authentication and authorization are delegated to Keycloak instead of being implemented directly inside the application.

This allows the platform to rely on standardized identity protocols.

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

Key security principles include:

centralized authentication;

OAuth2;

OpenID Connect;

PKCE for the Angular SPA;

JWT-based access tokens;

role-based authorization;

separation between public and internal services;

HTTPS termination through Nginx;

no direct exposure of databases or internal middleware to the Internet.

🌐 Network & Exposure Model

Only the required entry points are exposed publicly.

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

Services such as PostgreSQL, Redis, Kafka and MinIO are not intended to be directly reachable from the public Internet.

📦 Data & Storage Strategy

Different storage technologies are used according to the type of workload.

PostgreSQL

Used for transactional and relational application data.

Business entities
Users
Training data
Consultations
Certificates
Application relationships
        │
        ▼
    PostgreSQL

Redis

Used for fast-access and temporary data where caching is justified.

Application
    │
    ├── Database access
    │
    └── Redis cache

This reduces unnecessary database access for suitable workloads.

MinIO

MinIO provides centralized object storage.

Instead of keeping uploaded files inside application containers:

Old approach

Microservice
    │
    └── Local /uploads directory

the target architecture is:

Microservices
     │
     ▼
    MinIO
     │
     ├── user objects
     ├── training resources
     ├── certificates
     └── application files

This improves:

persistence;

portability;

backup management;

separation between application runtime and file storage.

⚡ Event-Driven Communication

Kafka is used for workflows where asynchronous communication provides value.

Producer Service
       │
       │ Event
       ▼
     Kafka
       │
       ├──────────► Consumer A
       │
       └──────────► Consumer B

Using asynchronous events helps reduce direct coupling between services and prepares the platform for workflows that do not require synchronous request/response communication.

Kafka is treated as infrastructure state and uses persistent storage independently from MinIO.

🔄 Service Discovery & Configuration

QualeanPro includes dedicated infrastructure services for configuration and discovery.

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

This allows application services to avoid hard-coded service locations and centralizes environment-specific configuration.

🐳 Containerized Architecture

The production platform runs using Docker containers.

Each major component is isolated into its own container:

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

Containerization provides:

consistent runtime environments;

reproducible deployments;

service isolation;

simplified dependency management;

easier rollback and replacement;

resource limits per service.

🧠 Container Resource Management

Production operation also requires controlling CPU and memory consumption.

Java services are monitored independently because JVM-based workloads can consume memory beyond the Java heap.

The production environment therefore considers:

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

This is an example of the transition from application development to real production operations.

💾 Persistent Volume Strategy

Stateful services use Docker volumes.

The persistence strategy covers components such as:

PostgreSQL
Keycloak
Redis
Kafka
MinIO

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

This improves maintainability and operational traceability.

🚀 CI/CD Pipeline

QualeanPro uses GitHub Actions to automate deployment workflows.

A simplified pipeline looks like:

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

This makes deployments easier to trace:

Git Commit
    │
    ▼
Docker Image Tag
    │
    ▼
Production Deployment

A production version can therefore be associated with the source revision that generated it.

🌐 Reverse Proxy & HTTPS

Nginx is the public entry point of the platform.

Responsibilities include:

HTTPS termination;

frontend delivery;

API routing;

security headers;

reverse proxying;

separation between public endpoints and internal services.

Client
  │
  │ HTTPS
  ▼
Nginx
  │
  ├────────► Angular Frontend
  │
  └────────► API Gateway

TLS certificates are managed separately from the application containers.

📊 Observability

Production systems need more than functional code.

QualeanPro includes an observability layer for understanding runtime behavior.

Applications
    │
    ├── Metrics
    ├── Logs
    └── Health Information
          │
          ▼
     Observability Stack
          │
          ├── Prometheus
          ├── Grafana
          └── Logging Pipeline

The monitoring strategy covers areas such as:

container availability;

service health;

memory usage;

CPU usage;

infrastructure status;

application metrics;

disk utilization;

service failures.

❤️ Health Checks

Docker health checks are used for critical components and application services.

Example operational states:

Service
   │
   ├── starting
   │
   ├── healthy
   │
   └── unhealthy

Health checks help distinguish:

Container running
        ≠
Application ready

This is particularly important for databases, identity services and Spring Boot applications.

💾 Backup & Recovery Strategy

Persistent application data requires an explicit recovery strategy.

The main data domains requiring protection include:

PostgreSQL
    │
    └── transactional data

MinIO
    │
    └── object storage

The operational approach includes:

scheduled backups;

retention policies;

backup verification;

separation between live data and backups;

recovery documentation;

disaster-recovery planning.

A backup is considered useful only if restoration has been considered as part of the process.

🧪 Production Operations

Operating QualeanPro in production involves tasks beyond application development.

Examples include:

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

A typical maintenance validation flow is:

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

🧯 Real Engineering Challenges

Building and operating the platform required solving several real integration and production issues.

CORS Configuration

Frontend and API communication required correctly aligning:

Browser
Angular
Nginx
Gateway
Backend services

Incorrect CORS configuration could block valid requests even when backend services were operational.

Keycloak Redirect Configuration

Authentication flows required correct redirect URI and client configuration.

A typical issue:

invalid_redirect_uri

required understanding the relationship between:

Angular SPA
     │
     ▼
Keycloak Client
     │
     ▼
Configured Redirect URI

Container DNS & Networking

Dockerized services communicate through container networks and service names.

Errors such as:

UnknownHost

required validating:

Docker network membership;

service names;

Compose configuration;

container health;

startup dependencies.

Database Availability

Stateful services need to be ready before dependent applications can operate correctly.

This required:

health checks;

retry strategies;

startup dependency management;

database diagnostics.

Memory Pressure

Java microservices can approach their Docker memory limits even when the host still has available RAM.

This required distinguishing:

Host RAM
      vs
Container RAM Limit
      vs
JVM Heap

and treating memory allocation as an operational engineering concern.

Persistent Storage

Legacy upload volumes and anonymous Docker volumes required a controlled migration strategy.

The migration principle is:

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

🧠 Key Engineering Decisions

Why Microservices?

Microservices were chosen to isolate major business capabilities and allow services to evolve independently.

The approach also provides practical experience with:

distributed communication;

service discovery;

centralized configuration;

container orchestration concepts;

independent deployment;

operational observability.

Why Keycloak?

Authentication is security-sensitive and should not be reinvented without a strong reason.

Keycloak provides:

standardized protocols;

centralized identity management;

OAuth2;

OpenID Connect;

token management;

role-based authorization.

Why Kafka?

Kafka is used where asynchronous communication and decoupling provide architectural value.

It is not intended to replace synchronous APIs for every interaction.

Why Redis?

Redis is used selectively for ephemeral or cacheable data.

The goal is not to introduce infrastructure unnecessarily, but to use it where fast temporary access provides measurable value.

Why MinIO?

Application containers should remain disposable.

Files should therefore not depend on the lifecycle of a specific application container.

MinIO provides dedicated object storage independent from microservice runtime containers.

Why Docker?

Docker provides reproducibility between environments and isolates service dependencies.

It also establishes a foundation for future container orchestration.

📐 Engineering Principles

Several principles guide the project:

Separation of Concerns
        │
        ├── Business services
        ├── Identity
        ├── Persistence
        ├── Messaging
        ├── Object storage
        └── Observability

Infrastructure as replaceable components

Application containers as disposable workloads

Persistent state separated from runtime

Secure-by-default network exposure

Automation before manual deployment

Observability as part of architecture

Production operations as part of software engineering

📈 Current Technical Evolution

QualeanPro continues to evolve beyond its initial production architecture.

Areas under development or planned evolution include:

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

These items represent the evolution roadmap and should not be interpreted as all being currently available in production.

🤖 AI & RAG Exploration

The platform also serves as an environment for exploring AI-assisted capabilities.

A potential RAG architecture follows:

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

Technologies being explored include:

Spring AI;

LangChain4j;

Ollama;

PostgreSQL with pgvector.

🗺️ Architecture Evolution

The current platform provides a foundation for a future evolution toward a more complete cloud-native architecture.

CURRENT

Ubuntu Server
    │
Docker Compose
    │
Microservices


TARGET EVOLUTION

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

The objective is not to introduce Kubernetes simply for complexity, but to adopt orchestration when operational requirements justify it.

🎓 What This Project Demonstrates

QualeanPro demonstrates practical experience across the complete software lifecycle:

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

The project represents experience not only in building application features, but also in making software deployable, observable, maintainable and operable in production.

📁 Case Study Repository

This repository contains only public, non-sensitive engineering material.

Planned structure:

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

🔒 Confidentiality

QualeanPro is a private project.

The production source code is intentionally not published in this repository.

This public case study does not expose:

proprietary source code;

credentials;

API secrets;

private keys;

production environment variables;

internal infrastructure addresses;

database dumps;

customer or user data;

sensitive business information;

confidential operational configuration.

Only architecture concepts and non-sensitive engineering information are presented.

📌 Project Information

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

👨‍💻 Engineering Areas Demonstrated

Java Spring Boot Angular Microservices Distributed Systems
REST APIs Kafka Redis PostgreSQL Keycloak OAuth2
OpenID Connect PKCE MinIO Docker Docker Compose
GitHub Actions Nginx Linux Prometheus Grafana
CI/CD DevOps Cloud-Native Production Operations

<p align="center">
  <strong>
    Building software is only the beginning.<br>
    Reliable software must also be secured, deployed, monitored, maintained and continuously improved.
  </strong>
</p>
