# Probe questions and concepts

Pick the few that fit the ticket. Ask one at a time.

## 1. Requirements
- Who or what triggers this, and how often? (volume, bursts)
- What does "correct" mean here? What is the worst wrong result?
- How fast must it be? Is a user waiting, or is it a background job?
- Does anything already do part of this?

Concepts: functional vs non-functional requirements, back-of-envelope estimation, latency vs throughput, sync vs async.

## 2. Scope
- What will you explicitly not build?
- What are you assuming that nobody told you?
- What is the smallest version that closes the ticket?

Concepts: non-goals, assumptions as risks, incremental delivery.

## 3. Data and interfaces
- What are the entities and who owns each one?
- What is the key? What is unique? What gets queried, and by what?
- Which index does that query need?
- What does the caller send, what comes back, what are the error cases?
- Can this be called twice? What happens?

Concepts: normalization, primary and foreign keys, indexes, schema migrations, API contracts, idempotency, pagination, backwards compatibility.

## 4. Flow
- Walk one request from trigger to result. Where does it cross a process or network boundary?
- Where is state stored between steps?
- What runs in parallel, and what must be ordered?

Concepts: request lifecycle, queues, workers, caching, transactions, ordering, event vs request-response.

## 5. Deep dive
- What is the one part most likely to go wrong? Design it fully.
- Two writers touch the same row at once. What happens?
- 100x the data or traffic: what breaks first?
- A step fails halfway. What state is left behind?

Concepts: race conditions, locking and optimistic concurrency, N+1 queries, transactions and atomicity, retries with backoff, backpressure, consistency vs availability.

## 6. Tradeoffs and failure
- What did you pick, what did you reject, and why?
- How would you know in production that this is broken? (logs, metrics, alerts)
- How do you roll it back? Is the data migration reversible?
- What does a dependency being down do to you?

Concepts: tradeoff reasoning, observability, feature flags, safe rollout, blast radius, graceful degradation, timeouts and circuit breakers.

## Stretch round (greenfield, 100x)

1. Scale math
- How many of these happen per day, and so how many per second at peak?
- How big is one record, and how much storage is that per year?
- Is this read-heavy or write-heavy?

Concepts: back-of-envelope estimation, peak vs average, read/write ratio, storage growth.

2. First bottleneck
- What resource runs out first: the database, one server, a third-party limit?
- Which fix fits: cache, queue, read replica, more workers, partitioning?
- What does that fix cost you?

Concepts: caching and invalidation, queues and workers, replication and lag, sharding, rate limits, load balancing.

3. New failure mode
- With many machines, what can now happen that could not on one?
- One dependency is slow, not down. What happens to everything waiting on it?
- The same message is processed twice. What breaks?

Concepts: partial failure, timeouts, retry storms, at-least-once delivery, idempotency, hot keys.

4. Interview score
Rubric: requirements, structure, scale math, tradeoffs, clarity of explanation.
