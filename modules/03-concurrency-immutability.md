# Module 03 — Multithreading, Concurrency, and Immutability

## Why It Matters

Spring Boot applications process many requests concurrently.

A bug that never appears locally can become obvious under production traffic.

---

# Core Concepts

## Race Condition

```java
private int count = 0;

public void increment() {
    count++;
}
```

`count++` is not one indivisible operation.

Multiple threads can overwrite each other's updates.

---

## Atomicity

An operation is atomic if it appears indivisible to other threads.

Examples:

- `AtomicInteger.incrementAndGet()`
- database atomic update
- synchronized critical section

---

## Visibility

A thread may not immediately observe another thread's write unless the program establishes the required memory visibility guarantees.

---

## volatile

Useful when:

- you need visibility;
- writes are simple;
- the variable does not participate in a larger compound invariant.

```java
private volatile boolean shutdown;
```

`volatile` does **not** make `count++` atomic.

---

## synchronized

Provides mutual exclusion and memory visibility.

```java
public synchronized void increment() {
    count++;
}
```

Use carefully. Large synchronized regions reduce concurrency.

---

## Locks

`ReentrantLock` gives more control:

- `tryLock`
- timed acquisition
- interruptible locking

---

## Atomic Types

```java
AtomicLong sequence = new AtomicLong();

long id = sequence.incrementAndGet();
```

Useful for simple atomic state changes.

---

# Concurrent Collections

Prefer concurrency-aware collections when shared mutation is required:

- `ConcurrentHashMap`
- `CopyOnWriteArrayList`
- blocking queues

Do not assume wrapping everything with synchronization is the best design.

---

# Executors

```java
ExecutorService executor =
    Executors.newFixedThreadPool(10);
```

Use pools rather than manually creating a large number of platform threads.

---

# CompletableFuture

```java
CompletableFuture<User> userFuture =
    CompletableFuture.supplyAsync(() -> userClient.getUser(id));

CompletableFuture<List<Order>> orderFuture =
    CompletableFuture.supplyAsync(() -> orderClient.getOrders(id));

return userFuture.thenCombine(orderFuture, UserDashboard::new).join();
```

Use concurrency when tasks are independent.

Do not parallelize work that stresses the same bottleneck.

---

# Virtual Threads

Java 21 supports virtual threads.

Useful mainly for high-concurrency, blocking I/O workloads.

```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    Future<String> result = executor.submit(() -> callRemoteService());
}
```

Virtual threads reduce the cost of blocking threads.

They do not make CPU-intensive work magically faster.

---

# Spring Singleton Beans

Spring beans are singleton-scoped by default.

Therefore this is dangerous:

```java
@Service
class CheckoutService {
    private String currentUser;
}
```

Multiple requests can mutate the same field.

Prefer stateless services.

---

# Immutability

Immutable objects:

- are simpler to reason about;
- are easier to share across threads;
- reduce accidental mutation;
- work well as DTOs and value objects.

```java
public record Price(BigDecimal amount, Currency currency) {}
```

For collections:

```java
this.items = List.copyOf(items);
```

---

# Thread Safety Checklist

Ask:

- Is mutable state shared?
- Who owns the state?
- Can the state be immutable?
- Can the database enforce correctness?
- Can we avoid cross-thread state entirely?
- What happens under simultaneous requests?

---

# Lab 1 — Inventory Race Condition

Create:

```java
class Inventory {
    private int stock = 10;
    void reserve() { ... }
}
```

Run 100 concurrent reservations.

Observe incorrect results.

Fix it using:

1. synchronized
2. AtomicInteger
3. database atomic update

Compare trade-offs.

---

# Lab 2 — API Fan-Out

Call three simulated services:

- profile service
- order service
- recommendation service

Measure:

- sequential latency
- CompletableFuture latency
- virtual-thread approach

---

# Interview Questions

1. Thread vs process?
2. Race condition?
3. Atomicity vs visibility?
4. `volatile` vs `synchronized`?
5. `synchronized` vs `Lock`?
6. What makes an object immutable?
7. Why are Spring singleton beans usually stateless?
8. What are virtual threads?
9. When is parallelism harmful?
10. How would you prevent double stock reservation?
