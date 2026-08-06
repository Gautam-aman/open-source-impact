# Armeria (LINE) Contribution

## Project
Armeria — LINE's open-source HTTP/RPC microservice framework (Java)

## Pull Request
https://github.com/line/armeria/pull/6899

## Title
Fix NPE in Http1ObjectEncoder.doWriteReset() When pendingWritesMap Is Sparse

## Problem

When an HTTP/1 connection is reset during pipelined request handling, `Http1ObjectEncoder.doWriteReset()` iterates over a contiguous range of request IDs `[minClosedId, maxIdWithPendingWrites]` to close out all pending write promises.

However, the pending writes map (an `IntObjectMap`) is sparse — not every ID in that range necessarily has an entry. Iterating the range and calling operations on the retrieved value without a null-guard caused a `NullPointerException` for IDs that had no pending writes.

## Investigation

I traced the NPE to the `doWriteReset()` loop, confirmed that the `IntObjectMap` stores only entries that were explicitly inserted, and verified that the iteration range could include IDs for which no write had ever been registered. Reading the Armeria and Netty source confirmed this as a latent bug triggered only under sparse pipeline conditions.

## Solution

- Added a null-guard inside the iteration loop to skip map entries that are `null`.
- Ensured that only existing pending writes receive the reset signal, while absent IDs are silently skipped.
- Added targeted test coverage for the sparse-map scenario to prevent future regressions.

## Impact

- Eliminated a crash-inducing NPE in HTTP/1 pipelined connection handling under sparse pending-write conditions.
- Hardened the connection reset path in Armeria's HTTP/1 encoder.
- Improved stability for services using HTTP/1 pipelining at high concurrency.

## Skills Demonstrated

- Java
- Armeria Framework
- HTTP/1 Protocol
- Netty
- Pipelining and Connection Lifecycle
- Defensive Null Handling
- Unit Testing

## Key Learning

Iterating a contiguous ID range over a sparse map requires null-guards even when the range bounds are derived from the map's own metadata. Always verify that every position in a range is guaranteed to be populated before dereferencing it.
