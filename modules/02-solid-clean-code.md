# Module 02 — SOLID, Clean Code, and Spring Architecture

# SOLID

## S — Single Responsibility Principle

A class should have one primary reason to change.

Bad:

```java
class OrderService {
    void createOrder() {}
    void sendEmail() {}
    void generatePdf() {}
    void chargeCard() {}
}
```

Better:

- `OrderService`
- `PaymentService`
- `NotificationService`
- `InvoiceService`

Do not over-split tiny behavior into dozens of meaningless classes.

---

## O — Open/Closed Principle

Software should be open for extension and closed for unnecessary modification.

Instead of:

```java
if (type.equals("CARD")) { ... }
else if (type.equals("GCASH")) { ... }
else if (type.equals("PAYPAL")) { ... }
```

Use a strategy:

```java
public interface PaymentProcessor {
    boolean supports(PaymentType type);
    PaymentResult pay(PaymentCommand command);
}
```

---

## L — Liskov Substitution Principle

A subtype should honor the behavioral expectations of its parent abstraction.

If calling a subtype causes surprising exceptions for normal parent behavior, the hierarchy may be wrong.

---

## I — Interface Segregation Principle

Prefer focused contracts.

Bad:

```java
interface Worker {
    void code();
    void approvePayroll();
    void driveTruck();
}
```

Split contracts by capability.

---

## D — Dependency Inversion Principle

High-level business logic should depend on abstractions.

```java
public interface NotificationPort {
    void send(Notification notification);
}
```

Infrastructure can implement it:

```java
@Component
class EmailNotificationAdapter implements NotificationPort {
    ...
}
```

---

# SOLID in Spring Boot

Constructor injection supports explicit dependencies.

```java
@Service
public class CheckoutService {
    private final PaymentGateway gateway;

    public CheckoutService(PaymentGateway gateway) {
        this.gateway = gateway;
    }
}
```

Avoid field injection.

---

# Recommended Package Structure

A practical feature-first structure:

```text
com.example.orders
├── order
│   ├── api
│   ├── application
│   ├── domain
│   └── infrastructure
├── customer
└── shared
```

This often scales better than one giant folder for all controllers, services, and repositories.

---

# Entity vs DTO

Do not expose persistence entities directly from REST controllers.

Reasons:

- lazy-loading surprises
- leaking internal schema
- security mistakes
- accidental over-posting
- API tightly coupled to database changes

Use request/response DTOs.

---

# Domain Logic Placement

Prefer:

```java
order.cancel(reason);
```

over:

```java
orderService.setStatus(order, CANCELLED);
```

when the rule belongs naturally to the domain object.

---

# Clean Code Heuristics

Good code generally has:

- small focused methods;
- meaningful names;
- explicit dependencies;
- minimal side effects;
- clear error behavior;
- few hidden assumptions.

Avoid premature abstraction.

A duplicated 5-line block may be cheaper than the wrong generic framework.

---

# Lab — Refactor a God Service

Start with one service that:

- reads an order;
- validates stock;
- calculates price;
- saves the order;
- sends email;
- publishes an event.

Refactor into:

- domain logic
- application orchestration
- persistence adapter
- message publisher
- notification port

Then answer:

1. Which code changed because of SRP?
2. Which behavior became extensible through OCP?
3. Where is DIP visible?
4. Did the refactor actually improve readability?

---

# Interview Questions

1. Explain SOLID without definitions only.
2. Give one real Spring Boot example of DIP.
3. Why can too many interfaces be harmful?
4. What is an anemic domain model?
5. What belongs in a controller?
6. Why avoid returning JPA entities directly?
7. Layered architecture vs hexagonal architecture?
8. When would you intentionally keep logic simple instead of abstracting?
