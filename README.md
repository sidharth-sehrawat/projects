# GKE GitOps Microservices Platform

Production-style cloud-native microservices deployment on Google Kubernetes Engine (GKE) using GitOps, ArgoCD, Helm, Terraform, PostgreSQL, Redis, and Artifact Registry.

## Project Overview

This repository contains a complete end-to-end deployment of a distributed voting application running on Google Cloud Platform.

The platform demonstrates:

* Kubernetes application deployment
* GitOps with ArgoCD
* Infrastructure as Code with Terraform
* Stateful workloads using PostgreSQL
* Redis-based asynchronous processing
* Container image management using Artifact Registry
* Multi-namespace Kubernetes architecture
* Helm-based application packaging

---

## Architecture

```text
User
 │
 ▼
Vote Service (Flask)
 │
 ▼
Redis Queue
 │
 ▼
Worker Service (.NET)
 │
 ▼
PostgreSQL
 │
 ▼
Result Service (NodeJS)
```

GitOps Deployment Flow:

```text
Developer
    │
    ▼
GitHub
    │
    ▼
ArgoCD
    │
    ▼
GKE Cluster
```

---

## Repository Structure

```text
projects/
│
├── example-voting-app
│   ├── vote
│   ├── worker
│   └── result
│
├── example-voting-app-gitops
│   ├── argocd
│   ├── postgres
│   ├── redis
│   ├── vote
│   ├── worker
│   └── result
│
└── example-voting-app-infra
    ├── bootstrap
    ├── environments
    └── modules
```

---

## Components

### Application Repository

Contains application source code:

* Vote Service (Python / Flask)
* Worker Service (.NET)
* Result Service (NodeJS)

Path:

```text
example-voting-app/
```

### GitOps Repository

Contains:

* Helm charts
* Kubernetes manifests
* ArgoCD applications
* Namespace-specific deployments

Path:

```text
example-voting-app-gitops/
```

### Infrastructure Repository

Contains Terraform code for:

* VPC
* GKE Cluster
* Node Pools
* Artifact Registry
* IAM
* Workload Identity

Path:

```text
example-voting-app-infra/
```

---

## Kubernetes Namespaces

```text
vote
worker
redis
postgres
result
argocd
```

---

## Technologies Used

### Cloud

* Google Cloud Platform (GCP)
* Google Kubernetes Engine (GKE)
* Artifact Registry

### Infrastructure

* Terraform
* Helm

### GitOps

* ArgoCD

### Databases

* PostgreSQL
* Redis

### Languages

* Python
* C#
* JavaScript

### Containers

* Docker
* Kubernetes

---

## Current Status

Completed:

* GKE Cluster Provisioning
* Terraform Infrastructure Modules
* Artifact Registry Integration
* PostgreSQL StatefulSet Deployment
* Redis Deployment
* Vote Service Deployment
* Worker Service Deployment
* Result Service Deployment
* ArgoCD GitOps Automation
* Multi-Namespace Architecture

Planned:

* Ingress & Load Balancer
* Prometheus Monitoring
* Grafana Dashboards
* Centralized Logging
* Network Policies
* CI/CD Automation
* Security Hardening

---
