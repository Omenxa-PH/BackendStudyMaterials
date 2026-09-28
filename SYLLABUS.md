# 12-Week Java + Spring Boot Backend Engineer Syllabus

## Learning Goal

Build production-grade backend knowledge around Java 21 and Spring Boot while mastering the concepts commonly expected from mid-to-senior backend engineers.

---

## Week 1 — Java Core and OOP

Study:

- classes, objects, interfaces, abstract classes
- inheritance vs composition
- generics
- collections
- equals/hashCode
- records
- exceptions
- Optional
- streams
- lambdas

Build:

- small order-processing domain model
- custom exceptions
- immutable DTOs using records
- collection transformation exercises

Read:

- [Module 01](modules/01-java-core-oop.md)

Checkpoint:

- Explain `HashMap` lookup at a high level.
- Explain why `equals()` and `hashCode()` must agree.
- Explain composition vs inheritance.

---

## Week 2 — SOLID and Clean Architecture

Study:

- SRP
- OCP
- LSP
- ISP
- DIP
- dependency inversion in Spring
- package structure
- service boundaries
- DTO vs entity
- domain logic placement

Build:

- refactor one “god service”
- introduce strategy interfaces
- remove hard-coded external dependencies

Read:

- [Module 02](modules/02-solid-clean-code.md)

Checkpoint:

- Identify a SOLID violation from existing code.
- Explain why “more interfaces” does not automatically mean better design.

---

## Week 3 — Multithreading and Immutability

Study:

- threads and executors
- race conditions
- visibility
- atomicity
- synchronization
- locks
- concurrent collections
- CompletableFuture
- virtual threads
- immutable objects

Build:

- thread-safe inventory counter
- concurrent API fan-out
- benchmark sequential vs concurrent workloads

Read:

- [Module 03](modules/03-concurrency-immutability.md)

Checkpoint:

- Explain `volatile` vs `synchronized`.
- Explain why Spring singleton beans must usually be stateless.
- Explain when virtual threads help.

---

## Week 4 — Spring Boot Core

Study:

- IoC / DI
- bean lifecycle
- component scanning
- configuration properties
- profiles
- auto-configuration
- Actuator
- MVC request lifecycle
- configuration management

Build:

- clean layered Spring Boot service
- profile-specific configuration
- configuration validation

Read:

- [Module 04](modules/04-spring-boot-core.md)

Checkpoint:

- Explain what Spring actually injects.
- Explain constructor injection.
- Explain singleton bean scope.

---

## Week 5 — REST APIs, Validation, and Error Handling

Study:

- HTTP methods
- status codes
- resource-oriented API design
- validation
- exception handlers
- pagination
- API versioning
- DTO design
- Problem Details

Build:

- customer/order REST API
- global exception handling
- pagination and filtering
- request validation

Read:

- [Module 05](modules/05-rest-validation-errors.md)

Checkpoint:

- Explain PUT vs PATCH.
- Explain 400 vs 404 vs 409 vs 422.
- Explain why entities should not usually be exposed directly.

---

## Week 6 — Database, JPA, SQL, and Transactions

Study:

- entity lifecycle
- lazy/eager loading
- N+1 problem
- joins
- indexes
- transactions
- isolation
- optimistic/pessimistic locking
- pagination
- query tuning

Build:

- PostgreSQL-backed service
- transaction boundary exercise
- optimistic locking example
- query performance exercise

Read:

- [Module 06](modules/06-data-jpa-transactions.md)

Checkpoint:

- Explain `@Transactional`.
- Explain the N+1 problem.
- Explain optimistic locking.

---

## Week 7 — Streaming and Messaging

Study:

- queue vs topic
- RabbitMQ vs Kafka
- producer/consumer
- acknowledgements
- retries
- DLQ
- ordering
- at-least-once delivery
- consumer groups
- event contracts
- outbox pattern

Build:

- order-created event
- asynchronous inventory consumer
- retry + DLQ
- duplicate-event handling

Read:

- [Module 07](modules/07-streaming-messaging.md)

Checkpoint:

- Explain why “exactly once” is often misunderstood.
- Explain how duplicate messages happen.
- Explain queue vs log-based streaming.

---

## Week 8 — Caching and Idempotency

Study:

- local cache
- distributed cache
- cache-aside
- TTL
- invalidation
- stale data
- Redis
- Caffeine
- idempotency keys
- deduplication
- request fingerprints

Build:

- cached product lookup
- cache invalidation
- idempotent payment/order endpoint
- message deduplication table

Read:

- [Module 08](modules/08-caching-idempotency.md)

Checkpoint:

- Explain cache-aside.
- Explain the “two hard things” problem of cache invalidation.
- Explain how an idempotency key works.

---

## Week 9 — Security, TLS, JWT, OAuth2

Study:

- authentication vs authorization
- password hashing
- TLS
- mTLS
- JWT
- access/refresh tokens
- OAuth2
- OIDC
- CSRF
- CORS
- Spring Security filters
- method authorization

Build:

- JWT-protected API
- role-based endpoints
- refresh-token flow
- resource server configuration

Read:

- [Module 09](modules/09-security.md)

Checkpoint:

- Explain OAuth2 without saying “OAuth is authentication.”
- Explain JWT signature vs encryption.
- Explain why HTTPS is still required when using JWT.

---

## Week 10 — Design Patterns

Focus patterns:

- Factory
- Strategy
- Decorator
- Singleton
- Observer
- Adapter
- Template Method

Build:

- payment processor strategies
- notification factory
- decorated pricing calculation
- event observer example

Read:

- [Module 10](modules/10-design-patterns.md)

Checkpoint:

- Identify when Strategy is better than `if/else`.
- Explain why Spring beans often remove the need to manually implement Singleton.
- Explain Observer vs messaging broker.

---

## Week 11 — Testing and TDD

Study:

- unit tests
- integration tests
- slice tests
- mocks
- stubs
- test doubles
- Testcontainers
- TDD
- contract testing
- test pyramid

Build:

- unit tests for domain/service logic
- repository integration tests
- controller tests
- PostgreSQL Testcontainer
- RabbitMQ/Kafka Testcontainer if applicable

Read:

- [Module 11](modules/11-testing-tdd.md)

Checkpoint:

- Explain what should and should not be mocked.
- Explain Red → Green → Refactor.
- Explain why 100% coverage is not the goal.

---

## Week 12 — Observability, Performance, Deployment

Study:

- structured logs
- correlation IDs
- metrics
- tracing
- Actuator
- Micrometer
- profiling
- connection pools
- JVM memory
- Docker
- Kubernetes/OpenShift
- readiness/liveness probes
- CI/CD

Build:

- Actuator endpoints
- custom metrics
- Docker image
- health probes
- production checklist

Read:

- [Module 12](modules/12-observability-performance-deployment.md)

Checkpoint:

- Explain logs vs metrics vs traces.
- Explain readiness vs liveness.
- Explain why “works locally” does not mean production-ready.

---

# Final Project

Complete the [Capstone Project](CAPSTONE.md).

Recommended architecture:

- API service
- PostgreSQL
- Redis
- RabbitMQ/Kafka
- JWT/OAuth2 security
- async events
- idempotency
- caching
- observability
- Docker
- tests

---

# Weekly Routine

### Day 1
Concept study

### Day 2
Code examples

### Day 3
Hands-on lab

### Day 4
Refactoring and failure scenarios

### Day 5
Interview questions + notes + capstone integration

---

# Minimum Exit Criteria

Do not move on because you finished reading.

Move on when you can:

1. explain the topic;
2. build a small example;
3. test it;
4. describe one failure mode;
5. describe one trade-off;
6. relate it to a real Spring Boot application.
