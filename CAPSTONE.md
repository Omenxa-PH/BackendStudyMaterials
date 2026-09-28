# Capstone — Production-Style Order Processing Platform

Build one project that exercises the entire syllabus.

# Scenario

A customer places an order.

The system must:

1. validate the request;
2. prevent duplicate order creation;
3. save the order;
4. publish an event;
5. reserve inventory asynchronously;
6. update order state;
7. cache frequently read product data;
8. secure APIs;
9. expose health/metrics;
10. survive retries and duplicate messages.

---

# Suggested Architecture

```text
Client
  |
  v
API Gateway / Order API
  |
  +--> PostgreSQL
  |
  +--> Redis
  |
  +--> Message Broker
           |
           +--> Inventory Consumer
           |
           +--> Notification Consumer
```

---

# Required Technologies

- Java 21
- Spring Boot 3.x
- Maven
- PostgreSQL
- Redis
- RabbitMQ or Kafka
- Spring Security
- JWT/OAuth2 resource server
- JUnit 5
- Mockito
- Testcontainers
- Docker

Optional:

- OpenShift/Kubernetes
- Micrometer/Prometheus
- OpenTelemetry
- Flyway/Liquibase

---

# Features

## Order API

```text
POST /orders
GET /orders/{id}
POST /orders/{id}/cancel
GET /orders
```

POST `/orders` must accept:

```text
Idempotency-Key
```

---

# Order States

```text
PENDING
INVENTORY_RESERVED
CONFIRMED
FAILED
CANCELLED
```

Enforce valid transitions.

---

# Messaging

Events:

- OrderCreated
- InventoryReserved
- InventoryRejected
- OrderConfirmed

Every event should have:

- event ID
- event type
- timestamp
- correlation ID
- aggregate/order ID
- schema version

---

# Reliability Requirements

Implement:

- retries
- exponential backoff
- DLQ
- idempotent consumers
- outbox pattern
- duplicate-event handling

---

# Caching

Cache:

```text
GET /products/{id}
```

Track:

- cache hit
- cache miss

Evict/update cache after product changes.

---

# Security

At minimum:

- authenticated API
- USER role
- ADMIN role
- secure admin endpoint
- TLS in deployed environment

---

# Testing Requirements

Include:

- domain unit tests
- service tests
- controller tests
- PostgreSQL Testcontainer
- broker integration test
- duplicate request test
- duplicate message test
- authorization test

---

# Observability

Every request/event should be traceable by correlation ID.

Expose:

- health
- metrics
- custom order counter
- consumer failure counter

---

# Failure Scenarios to Demonstrate

1. duplicate POST
2. client timeout after successful order creation
3. broker temporarily unavailable
4. duplicate message delivery
5. malformed message
6. inventory service failure
7. DB conflict
8. Redis unavailable
9. expired JWT
10. unauthorized admin access

---

# Architecture Review Questions

When finished, explain:

1. Where is SOLID visible?
2. Which objects are immutable?
3. Where can concurrency occur?
4. How is idempotency implemented?
5. How are duplicate events handled?
6. What data is cached?
7. Why was that data chosen?
8. What happens if Redis fails?
9. What happens if the broker redelivers?
10. How does authentication work?
11. How does authorization work?
12. Where is TLS involved?
13. Which design patterns are used?
14. Which parts are unit tested?
15. Which parts use integration tests?
16. How would you scale the service?
17. What would you monitor in production?
18. What would you change at 10x traffic?
