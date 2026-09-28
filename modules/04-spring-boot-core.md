# Module 04 — Spring Boot Core

## Dependency Injection

Spring creates objects and wires dependencies.

Prefer constructor injection.

```java
@Service
public class OrderService {
    private final OrderRepository repository;

    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }
}
```

Benefits:

- explicit dependencies
- easier tests
- supports immutability
- prevents partially initialized objects

---

# Common Stereotypes

- `@Component`
- `@Service`
- `@Repository`
- `@Controller`
- `@RestController`
- `@Configuration`

They mostly participate in component scanning, but some also communicate architectural intent or add framework behavior.

---

# Bean Scopes

Common scopes:

- singleton
- prototype
- request
- session

Most services are singleton.

Do not keep request-specific mutable data in singleton fields.

---

# Configuration Properties

Prefer typed configuration:

```java
@ConfigurationProperties(prefix = "payment")
public record PaymentProperties(
        URI baseUrl,
        Duration timeout
) {}
```

Validate configuration at startup where possible.

---

# Profiles

Use profiles sparingly for environment-specific behavior.

Prefer external configuration for values.

Avoid maintaining completely different application behavior per environment unless necessary.

---

# Auto-Configuration

Spring Boot configures common infrastructure based on:

- classpath
- properties
- existing beans

Learn to ask:

> Which auto-configuration created this bean?

This is useful when debugging surprising behavior.

---

# Application Layers

Typical flow:

```text
Controller
   ↓
Application Service
   ↓
Domain
   ↓
Repository / External Port
```

Controllers should:

- parse HTTP concerns
- validate request shape
- call application logic
- return HTTP response

Controllers should not contain business workflows.

---

# Actuator

Useful production endpoints include:

- health
- info
- metrics
- loggers

Expose sensitive endpoints carefully.

---

# Spring Boot Startup Debugging

When an app fails to start:

1. read the first meaningful exception;
2. identify the failing bean;
3. inspect dependency chain;
4. inspect configuration;
5. check profile;
6. check missing environment variables;
7. check port/database/message broker availability.

---

# Lab

Create an application with:

- `OrderController`
- `OrderService`
- `OrderRepository`
- typed configuration properties
- dev/prod configuration
- Actuator

Add a fake external payment gateway configured through properties.

---

# Interview Questions

1. Spring vs Spring Boot?
2. What is IoC?
3. What is dependency injection?
4. Why constructor injection?
5. What is bean scope?
6. What is auto-configuration?
7. `@Component` vs `@Service`?
8. How does Spring find beans?
9. What is Actuator used for?
10. Why should singleton beans usually be stateless?
