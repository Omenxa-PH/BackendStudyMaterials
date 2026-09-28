# Module 06 — PostgreSQL, JPA, SQL, and Transactions

# Think SQL First

JPA is not a replacement for understanding SQL.

You should still understand:

- joins
- indexes
- execution plans
- constraints
- isolation
- locks
- pagination

---

# Entity Lifecycle

Common states:

- transient
- managed
- detached
- removed

Managed entities can be dirty-checked and persisted automatically inside a transaction.

---

# Lazy vs Eager

Defaulting everything to eager loading can cause huge object graphs.

Lazy loading can cause:

- extra queries
- `LazyInitializationException`
- N+1 queries

Fetch only what a use case needs.

---

# N+1 Problem

Example:

1 query for orders  
+ 1 query per order for customer/items.

Solutions may include:

- fetch join
- entity graph
- projections
- dedicated query
- batch fetching

---

# Transactions

```java
@Transactional
public void placeOrder(...) {
    ...
}
```

A transaction gives an atomic unit of database work.

Important:

- proxy-based behavior
- rollback rules
- transaction boundaries
- external calls inside transactions

Avoid holding database transactions open while waiting on slow network calls when possible.

---

# Isolation

Understand conceptually:

- Read Uncommitted
- Read Committed
- Repeatable Read
- Serializable

PostgreSQL typically uses Read Committed by default.

---

# Optimistic Locking

```java
@Version
private Long version;
```

Useful when conflicts are possible but uncommon.

If two writers edit the same record, one can fail with a version conflict.

---

# Pessimistic Locking

Locks database rows.

Useful in some high-contention correctness scenarios.

Costs:

- blocking
- deadlocks
- throughput reduction

---

# Indexes

An index can make reads faster but adds cost to:

- inserts
- updates
- storage

Index based on query patterns, not intuition only.

---

# Database Constraints

Use the database to enforce critical invariants where appropriate.

Examples:

- unique email
- not null
- foreign key
- check constraints

Application validation alone is not enough under concurrency.

---

# Lab

Create:

- `Order`
- `OrderItem`
- `Customer`

Implement:

- order listing
- order detail
- customer order history
- optimistic locking
- unique external order reference

Then inspect generated SQL.

---

# Performance Exercise

Create 100k rows.

Compare:

1. query without index
2. query with suitable index

Use `EXPLAIN ANALYZE`.

---

# Interview Questions

1. What does `@Transactional` do?
2. N+1 problem?
3. Lazy vs eager?
4. Optimistic vs pessimistic locking?
5. Why use DB constraints?
6. What is a composite index?
7. Why can too many indexes hurt?
8. What is transaction isolation?
9. Can a REST request create multiple transactions?
10. What happens if you call an external API inside a DB transaction?
