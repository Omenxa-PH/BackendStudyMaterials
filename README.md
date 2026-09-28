# Java + Spring Boot Backend Engineer Study Pack

A practical, production-oriented curriculum for becoming stronger in **Java 21 + Spring Boot 3.x backend engineering**.

This pack is organized around the topics from the backend-engineer checklist:

- SOLID design principles
- Multithreading
- Immutability
- Streaming and messaging
- Caching
- Idempotency
- Security
- SSL/TLS, JWT, OAuth2
- Factory, Decorator, Singleton, Observer patterns
- TDD

It also adds the surrounding skills needed to use those concepts well in real Spring Boot systems:

- REST API design
- Validation and error handling
- JPA, SQL, and transactions
- Resilience
- Observability
- Performance
- Docker/Kubernetes basics
- CI/CD thinking

## Recommended Stack

- Java 21
- Spring Boot 3.x
- Maven
- PostgreSQL
- Redis
- RabbitMQ or Kafka
- Docker / Docker Compose
- JUnit 5
- Mockito
- Testcontainers
- Spring Security
- Micrometer + Actuator

---

# Start Here

1. [Syllabus](SYLLABUS.md)
2. [Progress Checklist](PROGRESS_CHECKLIST.md)
3. [Java Core, OOP, and Collections](modules/01-java-core-oop.md)
4. [SOLID and Clean Code](modules/02-solid-clean-code.md)
5. [Concurrency and Immutability](modules/03-concurrency-immutability.md)
6. [Spring Boot Core](modules/04-spring-boot-core.md)
7. [REST, Validation, and Error Handling](modules/05-rest-validation-errors.md)
8. [Data, JPA, SQL, and Transactions](modules/06-data-jpa-transactions.md)
9. [Streaming and Messaging](modules/07-streaming-messaging.md)
10. [Caching and Idempotency](modules/08-caching-idempotency.md)
11. [Security: TLS, JWT, OAuth2](modules/09-security.md)
12. [Design Patterns](modules/10-design-patterns.md)
13. [Testing and TDD](modules/11-testing-tdd.md)
14. [Observability, Performance, and Deployment](modules/12-observability-performance-deployment.md)
15. [Capstone Project](CAPSTONE.md)
16. [Backend Interview Questions](INTERVIEW_QUESTIONS.md)
17. [Cheat Sheet](CHEATSHEET.md)

---

# Suggested Study Style

For each module:

1. **Read the concepts**
2. **Type the examples yourself**
3. **Build the lab**
4. **Break the lab intentionally**
5. **Debug it**
6. **Explain the topic without looking at notes**
7. **Answer the interview questions**
8. **Use the idea in the capstone**

A useful rule:

> Do not consider a topic learned until you can explain when **not** to use it.

---

# Time Commitment

### Fast track
2–3 hours/day, 5 days/week  
Approx. **8–10 weeks**

### Sustainable track
60–90 minutes/day, 5 days/week  
Approx. **12 weeks**

### Deep track
Study + implementation + interview preparation  
Approx. **16 weeks**

---

# What “Done” Looks Like

By the end, you should be able to:

- design a Spring Boot service without putting all logic in controllers;
- explain SOLID with Java examples;
- reason about race conditions and thread safety;
- use immutable objects where appropriate;
- build synchronous and asynchronous service flows;
- use RabbitMQ/Kafka safely;
- reason about retries and duplicate messages;
- design caching intentionally;
- create idempotent endpoints and consumers;
- secure APIs with JWT/OAuth2;
- understand the role of TLS;
- apply common design patterns naturally;
- write unit, integration, and containerized tests;
- diagnose performance and production issues;
- explain your architecture in an interview.

---

# Main Rule

This is not a memorization syllabus.

For every topic ask:

- What problem does it solve?
- What trade-off does it introduce?
- What breaks if I use it incorrectly?
- How would this behave under load?
- How would I test it?
- How would I observe it in production?
