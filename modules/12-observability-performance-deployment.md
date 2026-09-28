# Module 12 — Observability, Performance, Docker, Kubernetes, and CI/CD

# Observability

Three major signals:

- logs
- metrics
- traces

You usually need all three.

---

# Structured Logging

Prefer machine-searchable logs.

Include:

- timestamp
- service
- level
- request/correlation ID
- event/business ID
- error code

Do not log:

- passwords
- full tokens
- sensitive personal data

---

# Correlation ID

Pass the same ID through:

```text
API Gateway
  ↓
Service A
  ↓
RabbitMQ/Kafka
  ↓
Service B
```

This makes distributed debugging much easier.

---

# Metrics

Examples:

- request count
- latency
- error rate
- queue depth
- consumer lag
- DB pool usage
- cache hit rate

Avoid high-cardinality metric labels.

---

# Tracing

Distributed tracing helps answer:

> Where did the time go across services?

---

# Spring Boot Actuator

Useful endpoints:

- health
- metrics
- prometheus
- info

Secure management endpoints.

---

# Performance Method

Do not optimize blindly.

Use:

1. measurement
2. profiling
3. bottleneck identification
4. targeted change
5. re-measurement

---

# Common Bottlenecks

- slow SQL
- missing index
- N+1 queries
- external API latency
- undersized connection pools
- excessive serialization
- blocking calls
- retry storms
- cache misses
- GC pressure

---

# JVM Basics

Know conceptually:

- heap
- stack
- garbage collection
- allocation
- memory leak vs high allocation rate

---

# Docker

Minimal goals:

- reproducible build
- small image
- non-root runtime where practical
- external configuration
- health checks

---

# Kubernetes / OpenShift

Know:

- Deployment
- Pod
- Service
- ConfigMap
- Secret
- liveness probe
- readiness probe
- resource requests/limits
- horizontal scaling

---

# Readiness vs Liveness

## Readiness
Can this instance receive traffic?

## Liveness
Is this process healthy enough to keep running?

Bad liveness checks can create restart loops.

---

# CI/CD Pipeline

Typical pipeline:

```text
compile
  ↓
unit test
  ↓
integration test
  ↓
static/security checks
  ↓
build image
  ↓
deploy
  ↓
smoke test
```

---

# Production Readiness Checklist

Before deploy:

- config externalized
- secrets protected
- health endpoints working
- logs structured
- metrics available
- timeouts configured
- retries bounded
- DB migrations safe
- rollback strategy known
- idempotency considered
- alerts defined

---

# Lab

Containerize the capstone.

Add:

- Actuator
- custom metric
- correlation ID
- readiness probe
- liveness probe
- Docker Compose
- optional Kubernetes/OpenShift manifests

Run a load test and identify one bottleneck.

---

# Interview Questions

1. Logs vs metrics vs traces?
2. What is correlation ID?
3. Readiness vs liveness?
4. What causes retry storms?
5. Why set timeouts?
6. How do connection pools affect performance?
7. What happens when a pod is killed mid-request?
8. Why are resource limits useful?
9. What would you monitor on a message consumer?
10. How would you debug an API that became slow after deployment?
