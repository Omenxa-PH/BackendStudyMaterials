# Module 10 — Design Patterns for Java + Spring

Patterns are vocabulary, not goals.

Use a pattern because it makes the design clearer.

---

# 1. Strategy

Best for interchangeable behavior.

```java
public interface DiscountStrategy {
    Money apply(Money original);
}
```

Implementations:

- RegularDiscount
- VIPDiscount
- HolidayDiscount

Spring can inject all strategies:

```java
public PricingService(List<DiscountStrategy> strategies) {
    ...
}
```

Use Strategy to remove growing conditional trees.

---

# 2. Factory

Creates objects based on context.

```java
public class NotificationFactory {
    public NotificationSender create(Channel channel) {
        return switch (channel) {
            case EMAIL -> new EmailSender();
            case SMS -> new SmsSender();
        };
    }
}
```

In Spring, dependency injection often replaces manual object creation.

---

# 3. Decorator

Adds behavior without changing the wrapped type.

Example:

```text
BasePriceCalculator
   ↓ decorated by
DiscountCalculator
   ↓ decorated by
TaxCalculator
   ↓ decorated by
AuditCalculator
```

Useful for:

- logging
- metrics
- retries
- pricing rules
- validation layers

Spring AOP can also provide cross-cutting behavior, but it is not identical to the GoF Decorator pattern.

---

# 4. Singleton

One shared instance.

Spring singleton scope already manages a single bean instance per application context.

Do not write manual singleton code unless you truly need it.

Avoid mutable state in singleton beans.

---

# 5. Observer

One subject notifies many listeners.

In-process example:

- Spring application events

Distributed version:

- message broker / event bus

Do not confuse in-memory Observer with durable messaging.

---

# 6. Adapter

Wrap an incompatible external API behind your own interface.

```java
public interface PaymentGateway {
    PaymentResult charge(...);
}
```

```java
@Component
class StripePaymentAdapter implements PaymentGateway {
    ...
}
```

This keeps vendor code out of business logic.

---

# 7. Template Method

Base workflow with overridable steps.

Useful when a process is mostly fixed but a few steps vary.

Use with care; composition is often more flexible than inheritance.

---

# Patterns in Spring

Spring itself heavily uses patterns:

- Dependency Injection
- Proxy
- Factory
- Template Method
- Observer
- Adapter

Recognizing them helps you understand framework behavior.

---

# Lab

Create a checkout module using:

- Strategy → payment method
- Factory → notification sender
- Decorator → pricing calculation
- Adapter → external payment API
- Observer → order-completed notification

Then refactor one pattern out.

Ask:

> Was the design better before or after?

Patterns should earn their complexity.

---

# Interview Questions

1. Strategy vs Factory?
2. Decorator vs inheritance?
3. Singleton concerns?
4. Observer vs broker?
5. Adapter vs Facade?
6. Why can patterns be overused?
7. Which patterns are visible in Spring?
