# Module 11 — Testing, Testcontainers, and TDD

# Testing Pyramid

Typical balance:

```text
       few E2E tests
    more integration tests
 many fast unit tests
```

The exact shape depends on your system.

---

# Unit Test

Tests one unit of business logic in isolation.

```java
@Test
void rejectsOrderWhenStockIsInsufficient() {
    ...
}
```

Best targets:

- domain logic
- pricing rules
- validators
- pure services

---

# Mockito

Mock boundaries, not everything.

Good mock targets:

- external API client
- message publisher
- clock
- expensive dependency

Avoid mocking simple value objects.

---

# Integration Tests

Test real collaboration between parts.

Examples:

- repository + PostgreSQL
- controller + Spring MVC
- application + broker

---

# Testcontainers

Run real disposable infrastructure from tests.

Good for:

- PostgreSQL
- Redis
- RabbitMQ
- Kafka

This reduces the gap between fake tests and production behavior.

---

# Spring Test Slices

Examples:

- `@WebMvcTest`
- `@DataJpaTest`

Use them when the slice matches what you need.

Do not always boot the entire application.

---

# TDD Cycle

```text
RED
write a failing test

GREEN
write minimum code to pass

REFACTOR
improve design while tests remain green
```

TDD is primarily a design and feedback discipline.

---

# What to Test

Test:

- behavior
- business rules
- edge cases
- failure handling
- integration contracts

Avoid tests that only assert implementation details.

---

# Bad Test Smell

If a harmless refactor breaks dozens of tests, the tests may be too coupled to implementation.

---

# Contract Testing

Useful when multiple services depend on an API/message contract.

Protects teams from accidental incompatible changes.

---

# Lab

For the order service, write:

1. unit tests for total calculation
2. unit tests for order state transitions
3. repository integration test with PostgreSQL Testcontainer
4. controller validation test
5. message consumer integration test
6. duplicate-event test
7. security authorization test

---

# TDD Exercise

Feature:

> An order over ₱5,000 receives 5% discount unless already covered by a promo.

Do not write production code first.

Perform Red → Green → Refactor.

---

# Interview Questions

1. Unit vs integration test?
2. Mock vs stub?
3. What should be mocked?
4. What is TDD?
5. Why is 100% coverage not enough?
6. Why use Testcontainers?
7. What is contract testing?
8. How do you test async messaging?
9. How do you test idempotency?
10. What makes a test brittle?
