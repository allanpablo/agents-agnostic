---
name: pragmatic-observability
description: Minimal viable observability for real operations. Use for logs, monitoring, uptime checks, dashboards, production troubleshooting, and actionable alerting without overengineering.
allowed-tools: Read, Glob, Grep
---

# Pragmatic Observability

## Purpose

Use this skill to design observability that helps operators act quickly without building an unnecessarily heavy monitoring stack.

## Core Principles

1. Prefer actionable signal over dashboard volume.
2. Start with logs, uptime, and critical service health.
3. Add metrics when they answer operational questions.
4. Keep alerting low-noise and response-oriented.
5. Troubleshooting speed matters more than observability aesthetics.

## Minimum Viable Observability

- structured application logs
- system/service logs
- uptime checks
- health endpoints
- critical dependency visibility
- simple alerts for high-value failures

## Logging Rules

- Log key state transitions and failures.
- Include correlation IDs where workflows cross boundaries.
- Avoid logging secrets or unnecessary sensitive data.
- Make logs searchable by tenant, integration, and request when relevant.

## Metrics Rules

- Start with latency, error rate, throughput, and uptime.
- Track queue depth or retry accumulation for async flows.
- Add business metrics only when they support decisions.

## Alerting Rules

- Alert only on conditions that require action.
- Distinguish critical, warning, and informational paths.
- Prefer fewer alerts with clearer playbooks.

## Review Checklist

- [ ] Health checks exist
- [ ] Logs support production diagnosis
- [ ] Alerts are actionable
- [ ] Critical dependencies are visible
- [ ] Tenant/integration troubleshooting is possible
