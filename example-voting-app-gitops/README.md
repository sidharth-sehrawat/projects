# Example Voting App - GitOps Repository

This repository contains the GitOps deployment configuration for the Voting Application platform running on Google Kubernetes Engine (GKE).

Application source code is maintained separately. This repository serves as the single source of truth for Kubernetes deployments.

---

# Purpose

This repository is responsible for:

* Kubernetes Deployments
* StatefulSets
* Services
* Helm Charts
* ArgoCD Applications
* GitOps Synchronization

Any change committed to this repository is automatically reconciled by ArgoCD and deployed to the Kubernetes cluster.

---

# GitOps Workflow

```text
Developer
    │
    ▼
Git Push
    │
    ▼
GitHub Repository
    │
    ▼
ArgoCD
    │
    ▼
Kubernetes Cluster
```

ArgoCD continuously monitors this repository.

When a Helm chart or values file changes:

1. GitHub receives the commit
2. ArgoCD detects drift
3. ArgoCD renders Helm manifests
4. Kubernetes resources are updated
5. Cluster state matches Git state

---

# Repository Structure

```text
example-voting-app-gitops/
│
├── argocd/
│   └── applications/
│
├── vote/
│
├── worker/
│
├── result/
│
├── redis/
│
├── postgres/
│
├── monitoring/
│
└── vault/
```

---

# Components

## Vote

Frontend voting application.

Technology:

* Python
* Flask

Namespace:

```text
vote
```

---

## Worker

Background vote processor.

Technology:

* .NET

Namespace:

```text
worker
```

Responsibilities:

* Read votes from Redis
* Write votes to PostgreSQL

---

## Redis

Message queue between Vote and Worker services.

Namespace:

```text
redis
```

Responsibilities:

* Temporary vote storage
* Decoupling frontend from database writes

---

## PostgreSQL

Persistent vote storage.

Namespace:

```text
postgres
```

Deployment Type:

```text
StatefulSet
```

Persistent Storage:

```text
PersistentVolumeClaim
```

---

## Result

Results dashboard.

Technology:

* NodeJS
* Express
* Socket.IO

Namespace:

```text
result
```

Responsibilities:

* Read aggregated vote data
* Display live voting results

---

# Namespace Layout

```text
argocd
vote
worker
redis
postgres
result
```

Isolation is achieved using namespace boundaries.

---

# Helm Charts

Each component is deployed using an independent Helm chart.

Example:

```text
vote/
├── Chart.yaml
├── values.yaml
└── templates/
```

Benefits:

* Reusability
* Versioning
* Environment-specific customization
* GitOps compatibility

---

# ArgoCD Applications

Location:

```text
argocd/applications/
```

Applications managed:

```text
vote
worker
redis
postgres
result
```

Each application uses:

```yaml
syncPolicy:
  automated:
    prune: true
    selfHeal: true
```

This ensures cluster drift is automatically corrected.

---

# Operational Commands

Check application status:

```bash
kubectl get applications -n argocd
```

Check sync state:

```bash
kubectl get application vote -n argocd
```

Check workloads:

```bash
kubectl get pods -A
```

View logs:

```bash
kubectl logs deployment/vote -n vote
```

---

# Current Features

Implemented:

* ArgoCD GitOps
* Helm Deployments
* Redis Queue
* PostgreSQL StatefulSet
* Multi-Namespace Architecture
* Artifact Registry Images
* Automated Synchronization
* Self Healing Deployments

---

# Future Enhancements

* Ingress Controller
* External Load Balancer
* Prometheus
* Grafana
* Loki Logging
* Vault Integration
* Network Policies
* GitHub Actions CI Pipeline
* HPA Autoscaling

---

# Architecture

```text
Vote Service
     │
     ▼
Redis Queue
     │
     ▼
Worker Service
     │
     ▼
PostgreSQL
     │
     ▼
Result Service
```

