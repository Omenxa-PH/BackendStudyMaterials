# Module 08 — Caching and Idempotency

# Part A — Caching

## Why Cache?

Use caching to reduce:

- latency
- database load
- repeated computation
- external API calls

Do not cache because “Redis is fast.”

---

# Cache-Aside Pattern

```text
read request
   ↓
check cache
   ↓ miss
load from DB
   ↓
store in cache
   ↓
return
```

---

# Local vs Distributed Cache

## Caffeine
Fast in-process cache.

Pros:

- extremely low latency
- simple
- no network

Cons:

- each app instance has its own cache
- invalidation across replicas is harder

## Redis
Shared distributed cache.

Pros:

- shared state
- TTL
- richer data structures

Cons:

- network hop
- operational dependency
- serialization complexity

---

# Cache Invalidation

Common strategies:

- TTL expiration
- explicit delete on writes
- write-through
- event-driven invalidation
- versioned keys

Be careful with stale data.

---

# Cache Stampede

Many requests miss the same key and all hit the database.

Possible mitigations:

- request coalescing
- locking
- randomized TTL
- stale-while-revalidate

---

# Spring Cache

```java
@Cacheable(cacheNames = "products", key = "#id")
public ProductResponse getProduct(Long id) {
    return loadProduct(id);
}
```

Mutation:

```java
@CacheEvict(cacheNames = "products", key = "#id")
public void updateProduct(Long id, UpdateProductRequest request) {
    ...
}
```

Annotations are useful but do not remove the need to understand caching behavior.

---

# Part B — Idempotency

An operation is idempotent when performing it multiple times has the same intended business effect as performing it once.

---

# HTTP Idempotency

Naturally expected to be idempotent:

- GET
- PUT
- DELETE

POST is not automatically idempotent.

But you can design an idempotent POST.

---

# Idempotency Key

Client:

```http
POST /payments
Idempotency-Key: 5c8a...
```

Server stores:

```text
key
request fingerprint
status
response
created_at
```

On retry:

- same key + same request → return stored result
- same key + different request → reject

---

# Payment Example

Without idempotency:

1. client sends charge
2. server charges card
3. response is lost
4. client retries
5. card charged twice

With idempotency, the retry returns the original result.

---

# Database Uniqueness as Idempotency

Sometimes the simplest solution is a unique business key:

```sql
unique(external_order_id)
```

This is especially useful against concurrent duplicate requests.

---

# Consumer Deduplication

Track event IDs.

```text
processed_messages
------------------
consumer_name
event_id
processed_at
```

Use a unique constraint on `(consumer_name, event_id)`.

---

# Lab 1 — Product Cache

Implement:

- `GET /products/{id}`
- Caffeine cache
- Redis alternative
- TTL
- eviction on update

Measure DB calls.

---

# Lab 2 — Idempotent Order Creation

Implement:

```text
POST /orders
Idempotency-Key: ...
```

Simulate:

- double-click
- timeout + retry
- simultaneous duplicate requests
- same key, different body

---

# Interview Questions

1. Local vs distributed cache?
2. Cache-aside?
3. What is stale data?
4. What is cache stampede?
5. When should you not cache?
6. What does idempotent mean?
7. How would you make POST idempotent?
8. How do idempotency keys work?
9. Why is a DB unique constraint useful?
10. How do you handle duplicate broker events?
