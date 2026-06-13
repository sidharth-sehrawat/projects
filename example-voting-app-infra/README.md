# Example Voting App Infrastructure

Terraform-based Infrastructure as Code (IaC) for deploying a production-style GitOps platform on Google Cloud Platform (GCP).

This repository provisions and manages:

* VPC Networking
* Google Kubernetes Engine (GKE)
* Artifact Registry
* Node Pools
* Service Accounts
* Workload Identity
* ArgoCD deployment foundation

---

# Architecture Overview

```text
Terraform
    │
    ▼
Google Cloud Platform
    │
    ├── VPC
    ├── Subnets
    ├── Artifact Registry
    ├── GKE Cluster
    ├── Node Pools
    └── IAM
```

Applications are deployed separately using the GitOps repository and ArgoCD.

---

# Repository Structure

```text
example-voting-app-infra/
│
├── bootstrap/
│
├── environments/
│   └── dev/
│
└── modules/
    ├── networking/
    ├── gke/
    ├── node-pools/
    ├── artifact-registry/
    ├── service-accounts/
    └── workload-identity/
```

---

# Bootstrap Layer

Location:

```text
bootstrap/
```

Purpose:

* Create Terraform backend resources
* Create remote state storage
* Prepare Terraform execution environment

Resources:

* GCS Bucket (Terraform State)
* Required IAM permissions

---

# Environment Layer

Location:

```text
environments/dev/
```

Purpose:

Deploy complete development environment.

Resources:

* Network
* GKE Cluster
* Node Pools
* Artifact Registry
* IAM Configuration

---

# Terraform Modules

## Networking

Path:

```text
modules/networking
```

Responsibilities:

* VPC Creation
* Subnet Creation
* IP Allocation

---

## GKE

Path:

```text
modules/gke
```

Responsibilities:

* Kubernetes Control Plane
* Cluster Configuration
* Regional Settings

---

## Node Pools

Path:

```text
modules/node-pools
```

Responsibilities:

* System Pool
* Application Pool
* Node Labels
* Scheduling Separation

Example:

```text
system-pool
app-pool
```

---

## Artifact Registry

Path:

```text
modules/artifact-registry
```

Responsibilities:

* Docker Image Storage
* Image Version Management

Repository:

```text
voting-app
```

---

## Service Accounts

Path:

```text
modules/service-accounts
```

Responsibilities:

* GCP IAM Service Accounts
* Least Privilege Access

---

## Workload Identity

Path:

```text
modules/workload-identity
```

Responsibilities:

* Kubernetes ServiceAccount ↔ GCP Service Account Mapping
* Secure API Access

---

# Cluster Layout

```text
GKE Cluster
│
├── System Node Pool
│
└── Application Node Pool
    ├── vote
    ├── worker
    ├── result
    ├── redis
    └── postgres
```

---

# Deployment Flow

```text
Terraform Apply
        │
        ▼
Infrastructure Created
        │
        ▼
ArgoCD Installed
        │
        ▼
GitOps Repository Synced
        │
        ▼
Applications Deployed
```

---

# Terraform Commands

Initialize:

```bash
terraform init
```

Plan:

```bash
terraform plan
```

Apply:

```bash
terraform apply
```

Destroy:

```bash
terraform destroy
```

---

# Current Features

Implemented:

* Modular Terraform Design
* GKE Cluster Provisioning
* Artifact Registry
* Dedicated Node Pools
* Workload Identity Foundation
* GitOps-Compatible Infrastructure

---

# Future Enhancements

* Ingress Controller
* External Load Balancer
* Prometheus
* Grafana
* Loki
* Vault
* External Secrets
* CI/CD Automation


