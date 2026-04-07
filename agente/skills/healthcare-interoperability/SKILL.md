---
name: healthcare-interoperability
description: Interoperability patterns for healthcare systems. Use for RIS, PACS, HIS, LIS, HL7, FHIR, clinical integrations, data normalization, and audit-safe healthcare workflows.
allowed-tools: Read, Glob, Grep
---

# Healthcare Interoperability

## Purpose

Use this skill when a task touches healthcare operations, clinical data exchange, or integration with legacy medical systems.

## Core Principles

1. Prefer integration over replacement.
2. Preserve traceability across every clinical or operational handoff.
3. Normalize data at boundaries, not inside every consumer.
4. Build for retries, reconciliation, and partial failure handling.
5. Treat healthcare data as operationally critical and audit-sensitive.

## Common Domains

- RIS
- PACS
- HIS
- LIS
- HL7 v2.x
- FHIR
- webhook-based exchange
- ETL pipelines
- clinical scheduling and result flows

## Design Rules

### Integration Boundaries
- Define the source system of truth explicitly.
- Separate ingestion, normalization, validation, and delivery.
- Keep adapter logic isolated from domain logic.
- Store enough metadata to replay, reconcile, and audit messages.

### Reliability
- Expect malformed payloads, duplicate events, and out-of-order delivery.
- Add idempotency where events or webhooks can repeat.
- Design fallback paths for external dependency failure.
- Prefer dead-letter or retry queues for critical integrations.

### Data Handling
- Preserve original payloads when legally and operationally appropriate.
- Map external standards into internal canonical structures.
- Keep terminology translation explicit.
- Favor structured and queryable records over opaque blobs.

### Security and Audit
- Enforce least privilege across integration accounts.
- Log integration events without leaking unnecessary sensitive data.
- Maintain correlation IDs and traceable processing status.
- Make operational diagnosis possible without manual forensics.

## Recommended Architecture Pattern

```text
Source System -> Adapter -> Validation -> Normalization -> Domain Workflow -> Delivery/Storage -> Audit Trail
```

## Review Checklist

- [ ] Source of truth identified
- [ ] Contract documented
- [ ] Retry/fallback path defined
- [ ] Idempotency considered
- [ ] Canonical model defined
- [ ] Audit trail preserved
- [ ] Security boundary documented
