# Java + Spring Boot Backend Cheat Sheet

# SOLID

- **S** — one main responsibility
- **O** — extend behavior without repeatedly editing stable code
- **L** — subtypes honor parent expectations
- **I** — focused interfaces
- **D** — business logic depends on abstractions

---

# Concurrency

`volatile`
- visibility
- not compound-operation atomicity

`synchronized`
- mutual exclusion
- visibility

`AtomicInteger`
- simple atomic updates

`ConcurrentHashMap`
- concurrent shared map

Virtual threads
- strong fit for high-concurrency blocking I/O
- not a CPU-speed multiplier

---

# Spring

Prefer:

```java
private final Dependency dependency;

public Service(Dependency dependency) {
    this.dependency = dependency;
}
```

Avoid request-specific mutable state in singleton beans.

---

# REST

- GET → read
- POST → create/command
- PUT → replace
- PATCH → partial update
- DELETE → delete

Status:

- 200 OK
- 201 Created
- 204 No Content
- 400 Bad Request
- 401 Unauthenticated
- 403 Forbidden
- 404 Not Found
- 409 Conflict
- 422 Semantic validation failure
- 429 Too Many Requests
- 500 Server failure

---

# JPA

Watch for:

- N+1
- lazy loading
- transaction boundaries
- long-running transactions
- missing indexes
- entity leakage to API

Use:

```java
@Version
private Long version;
```

for optimistic locking.

---

# Messaging

At-least-once delivery means:

> duplicates are possible.

Therefore:

- event IDs
- idempotent consumers
- retries
- DLQ
- observability

---

# Caching

Cache only when you know:

- what is expensive;
- how stale data may become;
- how invalidation works;
- what happens if cache is unavailable.

---

# Idempotency

For unsafe retries:

```text
Idempotency-Key
```

Persist:

- key
- request fingerprint
- status
- response

Use DB uniqueness when possible.

---

# Security

TLS:
- protects transport

JWT:
- signed token format
- not automatically encrypted

OAuth2:
- authorization framework

OIDC:
- identity layer on OAuth2

Access token:
- call APIs

Refresh token:
- obtain new access token

---

# Patterns

Strategy:
- interchangeable behavior

Factory:
- creation decision

Decorator:
- wrap with additional behavior

Singleton:
- one instance

Observer:
- notify subscribers

Adapter:
- translate external API into your interface

---

# TDD

```text
RED → GREEN → REFACTOR
```

Test behavior, not implementation details.

---

# Production

Always think about:

- timeout
- retry
- circuit breaker
- rate limit
- idempotency
- observability
- security
- rollback
- concurrency
- failure recovery
