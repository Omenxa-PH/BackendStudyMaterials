# Module 01 — Java Core, OOP, Collections, and Streams

## Objectives

Be comfortable enough with Java that Spring does not hide language fundamentals from you.

---

## 1. OOP Fundamentals

Know:

- encapsulation
- abstraction
- polymorphism
- inheritance
- composition

Prefer composition when the relationship is **has-a**, not **is-a**.

```java
public interface PaymentGateway {
    PaymentResult charge(Money amount);
}

public final class OrderService {
    private final PaymentGateway paymentGateway;

    public OrderService(PaymentGateway paymentGateway) {
        this.paymentGateway = paymentGateway;
    }
}
```

The service depends on behavior, not a concrete gateway.

---

## 2. Interface vs Abstract Class

Use an interface when you primarily want to define a contract.

Use an abstract class when implementations genuinely share state or reusable implementation.

Avoid creating interfaces purely because “enterprise Java uses interfaces.”

---

## 3. Records

Great for immutable data carriers.

```java
public record CreateOrderRequest(
        Long customerId,
        List<Long> productIds
) {}
```

Good uses:

- request DTOs
- response DTOs
- event payloads
- value objects

---

## 4. equals() and hashCode()

Rule:

> If two objects are equal according to `equals`, they must return the same `hashCode`.

Important for:

- HashMap
- HashSet
- caching keys
- persistence models

Be careful with JPA entities whose database IDs are assigned after persistence.

---

## 5. Collections

Understand the intent of:

| Type | Typical Use |
|---|---|
| ArrayList | indexed ordered data |
| LinkedList | rarely the best default |
| HashSet | uniqueness |
| TreeSet | sorted uniqueness |
| HashMap | key/value lookup |
| ConcurrentHashMap | shared concurrent map |
| ArrayDeque | stack/queue |

Know Big-O at a practical level.

---

## 6. Generics

```java
public interface Repository<T, ID> {
    Optional<T> findById(ID id);
    T save(T value);
}
```

Understand:

- `T`
- bounded types
- wildcards
- `? extends`
- `? super`

Remember PECS:

- Producer → `extends`
- Consumer → `super`

---

## 7. Exceptions

Use checked/unchecked exceptions intentionally.

For most Spring application/domain errors, unchecked exceptions are common.

```java
public class OrderNotFoundException extends RuntimeException {
    public OrderNotFoundException(Long id) {
        super("Order not found: " + id);
    }
}
```

Do not use exceptions for normal control flow.

---

## 8. Optional

Good:

```java
return repository.findById(id)
    .orElseThrow(() -> new OrderNotFoundException(id));
```

Avoid:

- `Optional` fields in entities
- `Optional` method parameters
- calling `.get()` without checking

---

## 9. Java Streams

Example:

```java
List<String> activeEmails = users.stream()
    .filter(User::active)
    .map(User::email)
    .distinct()
    .sorted()
    .toList();
```

Know:

- map
- filter
- flatMap
- reduce
- collect
- groupingBy
- partitioningBy

Do not turn every loop into a stream.

Readability wins.

---

## 10. Value Objects

Instead of passing raw primitives everywhere:

```java
public record EmailAddress(String value) {
    public EmailAddress {
        if (value == null || !value.contains("@")) {
            throw new IllegalArgumentException("Invalid email");
        }
    }
}
```

---

# Lab

Create an order domain containing:

- `Order`
- `OrderItem`
- `Money`
- `OrderStatus`
- `CustomerId`
- `ProductId`

Requirements:

- use records for suitable immutable values;
- use `BigDecimal` for money;
- validate invariants;
- compute order total;
- reject empty orders.

---

# Interview Questions

1. ArrayList vs LinkedList?
2. HashMap vs ConcurrentHashMap?
3. Why must equals and hashCode be consistent?
4. What is immutability?
5. When should you use Optional?
6. map vs flatMap?
7. interface vs abstract class?
8. inheritance vs composition?
9. why use BigDecimal for money?
10. what are Java records?

---

# Mastery Check

You are ready to move on when you can build the lab without looking at the examples.
