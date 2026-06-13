# Troubleshooting Log

## Issue 1

### Symptom

ArgoCD Application Healthy but no resources deployed.

### Root Cause

Empty Helm templates.

### Resolution

Created deployment.yaml and service.yaml templates.

---

## Issue 2

### Symptom

PostgreSQL CrashLoopBackOff.

### Error

```text
initdb: directory exists but is not empty
lost+found detected
```

### Root Cause

Mounted PVC directly into PostgreSQL data directory.

### Resolution

Configured:

```yaml
env:
  - name: PGDATA
    value: /var/lib/postgresql/data/pgdata
```

Deleted failed pod.

StatefulSet recreated successfully.

---

## Issue 3

### Symptom

Worker continuously printed:

```text
Waiting for db
```

### Root Cause

Worker expected service:

```text
db
```

Service deployed as:

```text
postgres
```

### Resolution

Renamed PostgreSQL service:

```text
db
```

and redeployed.

---

## Issue 4

### Symptom

Worker CrashLoopBackOff.

### Error

```text
Name or service not known
```

### Root Cause

Incorrect Redis/PostgreSQL DNS names.

### Resolution

Updated application code:

```text
redis.redis.svc.cluster.local

db.postgres.svc.cluster.local
```

Rebuilt image.

Updated Helm values.

ArgoCD synchronized deployment.

---

## Issue 5

### Symptom

Vote application returned HTTP 500.

### Error

```text
redis.exceptions.ConnectionError
```

### Root Cause

Vote application still referenced:

```text
redis
```

instead of Kubernetes DNS.

### Resolution

Updated Flask application:

```python
Redis(
    host="redis.redis.svc.cluster.local"
)
```

Built new image.

Updated Helm chart.

ArgoCD synchronized deployment.

---

## Lessons Learned

* Always verify Service DNS names.
* Always inspect logs before changing manifests.
* Stateful workloads require special storage handling.
* ArgoCD can show Healthy even when applications are misconfigured.
* Helm rendering should always be tested locally using:

```bash
helm template
```

