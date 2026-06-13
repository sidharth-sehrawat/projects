# Deployment Flow

## Infrastructure Deployment

```text
Terraform
     │
     ▼
VPC
     │
     ▼
GKE Cluster
     │
     ▼
Node Pools
     │
     ▼
Artifact Registry
```

---

## GitOps Deployment Flow

```text
Developer
     │
     ▼
Git Commit
     │
     ▼
GitHub Repository
     │
     ▼
ArgoCD
     │
     ▼
Helm Rendering
     │
     ▼
Kubernetes API Server
     │
     ▼
Cluster Resources
```

---

## Runtime Flow

```text
User
 │
 ▼
Vote Pod
 │
 ▼
Redis Service
 │
 ▼
Worker Pod
 │
 ▼
PostgreSQL Service
 │
 ▼
Result Pod
```

---

## Scheduling Flow

```text
Deployment
      │
      ▼
ReplicaSet
      │
      ▼
Scheduler
      │
      ▼
Node
      │
      ▼
Pod
```

---

## StatefulSet Flow

```text
StatefulSet
      │
      ▼
PVC
      │
      ▼
PV
      │
      ▼
Persistent Disk
```

