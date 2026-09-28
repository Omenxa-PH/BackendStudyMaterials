# Module 07 — Streaming, Messaging, RabbitMQ, Kafka, and IBM MQ Concepts

# Why Messaging?

Messaging helps decouple services in:

- time
- availability
- deployment
- workload processing

But it introduces:

- eventual consistency
- retries
- duplicates
- ordering complexity
- observability challenges

---

# Queue vs Stream

## Traditional Queue
A message is typically processed by one consumer from a competing-consumer group.

RabbitMQ and IBM MQ fit many queue-based workflows.

## Log / Stream
Events are retained and consumers track offsets.

Kafka is designed around this model.

---

# RabbitMQ Mental Model

```text
Producer
  ↓
Exchange
  ↓ routing
Queue
  ↓
Consumer
```

Concepts:

- direct exchange
- topic exchange
- fanout exchange
- routing key
- acknowledgement
- prefetch
- DLQ

---

# Kafka Mental Model

```text
Producer
  ↓
Topic
  ↓
Partitions
  ↓
Consumer Group
```

Ordering is typically guaranteed within a partition, not globally across all partitions.

---

# Delivery Semantics

## At-most-once
Possible loss, no duplicate retry.

## At-least-once
Messages may be delivered more than once.

Therefore consumers should often be idempotent.

## Exactly-once
Possible only under specific system boundaries and configurations.

Do not assume an entire distributed business workflow is globally “exactly once.”

---

# Acknowledgements

Acknowledge only when processing reached the point that should be considered successful.

If the consumer crashes before ack, a broker may redeliver.

This is normal.

Design for it.

---

# Retry Strategy

Good retries need:

- backoff
- maximum attempts
- retryable error classification
- dead-letter behavior

Do not retry:

- invalid schema forever
- permanent business rejection
- malformed input

---

# Dead Letter Queue

A DLQ is not a garbage bin.

You need an operational process:

- inspect
- classify
- repair
- replay
- alert

---

# Event Design

Prefer meaningful events:

```json
{
  "eventId": "uuid",
  "eventType": "OrderCreated",
  "occurredAt": "...",
  "orderId": "..."
}
```

Useful metadata:

- event ID
- correlation ID
- causation ID
- schema version

---

# Outbox Pattern

Problem:

1. save DB record
2. publish message

If one succeeds and the other fails, state can become inconsistent.

Outbox approach:

1. write domain state + outbox row in one transaction;
2. separate publisher forwards outbox record to broker;
3. mark as published.

---

# Consumer Idempotency

Store processed event IDs.

Pseudo-flow:

```text
if event_id already processed:
    acknowledge and stop

process business logic
record event_id
commit
acknowledge
```

Be careful that business work and dedupe state stay transactionally consistent.

---

# IBM MQ Perspective

IBM MQ is common in enterprise integration.

Concepts map naturally to:

- queues
- producers
- consumers
- durable delivery
- acknowledgements/transactions

When bridging old and new platforms, treat message contract and delivery semantics as first-class architecture concerns.

---

# Lab

Build:

```text
Order Service
   ↓ OrderCreated
Broker
   ↓
Inventory Service
   ↓ InventoryReserved
Broker
   ↓
Order Service
```

Requirements:

- correlation ID
- retry
- DLQ
- duplicate message protection
- structured logs
- failure simulation

---

# Failure Drills

Test:

1. consumer crashes after DB write but before ack;
2. duplicate event arrives;
3. broker unavailable;
4. malformed message;
5. downstream DB unavailable;
6. event received out of order.

---

# Interview Questions

1. RabbitMQ vs Kafka?
2. Queue vs topic?
3. What is a consumer group?
4. What causes duplicate messages?
5. What is a DLQ?
6. What is the outbox pattern?
7. Why should consumers be idempotent?
8. What is message ordering?
9. What is backpressure?
10. Why is distributed “exactly once” difficult?
