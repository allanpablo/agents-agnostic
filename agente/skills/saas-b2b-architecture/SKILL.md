---
name: saas-b2b-architecture
description: Pragmatic SaaS B2B architecture patterns. Use for multi-tenant systems, RBAC, billing-aware design, reusable modules, and product-ready backend structures.
allowed-tools: Read, Glob, Grep
---

# SaaS B2B Architecture

## Purpose

Use this skill when building systems that should be ready to evolve into product, especially with tenant-aware behavior and operational reuse.

## Core Principles

1. Think multi-tenant early, but implement only what current scope needs.
2. Keep tenant boundaries explicit in data, auth, and logs.
3. Build reusable modules instead of customer-specific sprawl.
4. Make RBAC and auditability first-class in product-critical flows.
5. Design for billing awareness when usage or entitlement may matter later.

## Default Preferences

- Modular monolith first
- PostgreSQL as primary system of record
- Explicit domain services
- Fastify + TypeScript for product backend
- Prisma when it improves delivery speed without hiding critical behavior

## Required Design Questions

- What defines a tenant?
- Which records are tenant-scoped vs global?
- What are the operator/admin roles?
- Where must audit logs exist?
- Which features may become plan- or billing-sensitive later?

## Recommended Boundaries

### Domain
- tenant
- user
- membership / role
- organization settings
- billing/plan awareness
- integrations
- audit events

### Technical
- API layer
- application services
- domain rules
- adapters / integrations
- persistence layer

## Anti-Patterns

- Single-tenant assumptions hidden in code paths
- RBAC added only in the UI
- Audit logs treated as optional
- Customer-specific branching in core domain logic
- Billing logic scattered across handlers

## Review Checklist

- [ ] Tenant model is explicit
- [ ] RBAC boundaries are defined
- [ ] Audit events identified
- [ ] Shared vs tenant data separated
- [ ] Product code avoids customer-specific sprawl
- [ ] Architecture is reusable and maintainable
