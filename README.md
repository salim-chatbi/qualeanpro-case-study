# QualeanPro — Cloud-Native E-Learning Platform

> **Public Engineering Case Study**  
> The production source code is private and is not included in this repository.

QualeanPro is a production-oriented e-learning platform designed to support training management, consultations, certification workflows, user management and online learning experiences through a modern **microservices architecture**.

This repository presents the engineering decisions, architecture, infrastructure and technical challenges behind the platform without exposing private source code or sensitive production information.

---

## 🎯 Project Overview

QualeanPro was designed to provide a scalable digital learning environment capable of supporting:

- user and profile management;
- training and course management;
- consultation services;
- certificate generation;
- Zoom session integration;
- authentication and authorization;
- asynchronous communication;
- object storage;
- monitoring and observability;
- CI/CD automation;
- production deployment.

The platform is built with a strong focus on:

- scalability;
- maintainability;
- security;
- observability;
- cloud-native practices;
- production reliability.

---

## 👨‍💻 My Role

I contributed to the design, development and production deployment of the platform across multiple technical areas.

### Backend Engineering

- Java and Spring Boot microservices
- REST API design
- service-to-service communication
- configuration management
- service discovery
- API gateway integration
- persistence with PostgreSQL
- asynchronous processing with Kafka
- caching with Redis

### Frontend

- Angular SPA integration
- authentication flow integration
- API communication through the gateway
- production frontend deployment

### Security

- Keycloak-based Identity and Access Management
- OAuth2
- OpenID Connect
- PKCE
- role-based access control
- secured application access

### DevOps & Production

- Docker and Docker Compose
- GitHub Actions CI/CD
- Nginx reverse proxy
- HTTPS/TLS
- production deployment on Ubuntu
- container resource management
- persistent volume management
- backup strategy
- monitoring and troubleshooting

### Observability

- Prometheus
- Grafana
- centralized logs
- service health checks
- production monitoring

---

## 🏗️ High-Level Architecture

```text
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
