---
name: integration-reliability
description: Reliability patterns for external and internal integrations. Use for webhooks, retries, idempotency, reconciliation, ETL safety, and failure-tolerant system boundaries.
allowed-tools: Read, Glob, Grep
---

# Integration Reliability

## Purpose

Use this skill when a task depends on external systems, unstable providers, asynchronous processing, or operational fallback.

## Core Principles

1. Assume external systems will fail, delay, duplicate, or drift.
2. Make retries safe through idempotent handling.
3. Separate transport failure from business rejection.
4. Design reconciliation instead of assuming perfect delivery.
5. Preserve enough state to recover without guesswork.

## Reliability Patterns

### Webhooks
- verify authenticity
- persist receipt before processing when appropriate
- return fast, process safely
- support replay and deduplication

### ETL / Scheduled Sync
- track checkpoints
- make runs resumable
- record partial failures
- expose reconciliation status

### External APIs
- add timeout, retry, circuit-breaker style thinking when warranted
- classify recoverable vs non-recoverable failures
- provide fallback or degraded mode when possible

## Operational Rules

- Correlate every integration execution.
- Keep operator-facing failure visibility.
- Prefer queues for unstable or bursty boundaries.
- Document contracts and failure behavior.

## Review Checklist

- [ ] Failure modes identified
- [ ] Retries are safe
- [ ] Idempotency considered
- [ ] Reconciliation path exists
- [ ] Operator visibility exists
- [ ] Fallback behavior defined
