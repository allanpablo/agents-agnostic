---
name: automation-ops
description: Operational automation design using pragmatic workflows. Use for n8n, service workflows, support automation, AI-assisted operations, and repeatable business process execution.
allowed-tools: Read, Glob, Grep
---

# Automation Ops

## Purpose

Use this skill for workflow automation with operational value, especially where repetitive work, support burden, or process latency can be reduced.

## Core Principles

1. Fix the process before automating it.
2. Automate repeated, rule-based, auditable work first.
3. Keep humans in the loop where risk is high.
4. Prefer simple, inspectable workflows over black-box magic.
5. Design automations as operational products, not temporary hacks.

## Default Stack Preference

- n8n as the primary automation layer
- Webhooks and APIs as first-class integration points
- AI nodes only with bounded prompts and validation
- Google Sheets only as support tooling, not authoritative core

## Workflow Design Rules

- Define trigger, processing, decision points, side effects, and fallback.
- Store execution status where operational visibility matters.
- Make retries explicit.
- Provide manual override for critical flows.
- Avoid hidden branching that operators cannot inspect.

## AI in Automation

- Use AI for triage, summarization, classification, and operator acceleration.
- Validate AI outputs before irreversible actions.
- Keep deterministic rules around AI steps.
- Add fallback paths for provider failure or ambiguous outputs.

## Review Checklist

- [ ] Process was simplified before automation
- [ ] Trigger and outcomes are explicit
- [ ] Failures are visible
- [ ] Manual override exists where needed
- [ ] AI steps are bounded and validated
