# Architecture

## Application Architecture

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

---

## Component Responsibilities

### Vote

Namespace:

```text
vote
```

Responsibilities:

* Receive votes
* Store votes in Redis queue
* Frontend application

Technology:

* Python
* Flask

---

### Redis

Namespace:

```text
redis
```

Responsibilities:

* Message queue
* Decouple frontend from database

Technology:

* Redis

---

### Worker

Namespace:

```text
worker
```

Responsibilities:

* Read votes from Redis
* Persist votes into PostgreSQL

Technology:

* .NET

---

### PostgreSQL

Namespace:

```text
postgres
```

Responsibilities:

* Persistent vote storage

Deployment:

```text
StatefulSet
```

Storage:

```text
PersistentVolumeClaim
```

---

### Result

Namespace:

```text
result
```

Responsibilities:

* Read vote counts
* Display live results

Technology:

* NodeJS
* Express
* Socket.IO

```
```

