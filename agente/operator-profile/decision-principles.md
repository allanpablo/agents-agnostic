# Decision Principles

## Core Heuristics

1. Resolve with the lowest complexity level that does not compromise future scale.
2. Prefer integration over replacement, especially in operational and healthcare environments.
3. Think multi-tenant and reusable by default when building product code.
4. Avoid closed tools lock-in when there is a practical open alternative.
5. Automate before expanding manual headcount.
6. Structured data is more valuable than cosmetically good but weakly governed data.
7. Security and traceability are mandatory, not optional add-ons.
8. Anything manual today should be a candidate for automation tomorrow.
9. Minimum viable monitoring comes before scaling complexity.
10. Practical performance beats theoretically perfect architecture.

## Trade-off Rules

### Architecture style
- Prefer: modular monoliths or clearly separated modules within a single deployable unit.
- Accept when needed: service separation around integration boundaries or operational isolation.
- Avoid by default: premature microservices and orchestration-heavy platforms.
- Trigger to escalate complexity: clear scaling, compliance, isolation, or ownership pressure.

### Typing strictness
- Prefer: strong typing in TypeScript, especially at domain and integration boundaries.
- Accept when needed: pragmatic looseness in glue code and automation layers.
- Avoid by default: weak contracts in critical business flows.
- Trigger to escalate complexity: external integrations, billing, RBAC, tenant logic, clinical data.

### Testing depth
- Prefer: focused high-signal tests on business logic, integrations, and failure paths.
- Accept when needed: lighter test coverage on low-risk UI details.
- Avoid by default: fragile or overly broad test suites with low operational value.
- Trigger to escalate complexity: money movement, access control, tenant isolation, healthcare workflows.

### Performance optimization
- Prefer: practical performance improvements with clear operational impact.
- Accept when needed: targeted caching, queues, and async processing.
- Avoid by default: speculative optimization and architecture inflation.
- Trigger to escalate complexity: observed latency, throughput bottlenecks, or user-facing degradation.

### DX vs runtime efficiency
- Prefer: developer experience that keeps systems maintainable and teams fast.
- Accept when needed: extra runtime complexity if it materially improves reliability or cost.
- Avoid by default: painful local/dev workflows in the name of premature optimization.
- Trigger to escalate complexity: sustained production pain, cost pressure, or compliance needs.

### Monolith vs services
- Prefer: modular monolith.
- Accept when needed: isolated workers, integration adapters, or boundary-specific services.
- Avoid by default: fragmented services with duplicated concerns.
- Trigger to escalate complexity: independent scaling or failure isolation requirements.

### SQL vs NoSQL
- Prefer: PostgreSQL-first with explicit schema and traceable data evolution.
- Accept when needed: Redis for speed, queues, cache, and event support.
- Avoid by default: polyglot persistence without a concrete reason.
- Trigger to escalate complexity: access pattern mismatch or operational proof that SQL alone is insufficient.

### Build vs buy
- Prefer: build the differentiating workflow, buy the commodity.
- Accept when needed: managed or closed tools that reduce operational burden significantly.
- Avoid by default: strategic dependence on tools that block portability.
- Trigger to escalate complexity: clear ROI, faster time to value, or reduced operational risk.

### Sync vs async workflows
- Prefer: sync flows for simplicity when latency and coupling are acceptable.
- Accept when needed: async flows for reliability, retries, and long-running processes.
- Avoid by default: event-driven sprawl without observability.
- Trigger to escalate complexity: third-party instability, high volume, or user-facing timeout risk.

### Automation vs manual control
- Prefer: automate repetitive, auditable, and rule-based work.
- Accept when needed: manual checkpoints for high-risk or low-frequency operations.
- Avoid by default: fully manual operational loops that can be standardized.
- Trigger to escalate complexity: repeated execution, SLA risk, or support burden.

## Decision Escalation

- Scale threshold: when tenant count, event volume, or integration load creates measurable bottlenecks.
- Team threshold: when ownership or change velocity suffers from too much coupling.
- Reliability threshold: when incidents, retries, and recovery need dedicated isolation.
- Compliance threshold: when auditability, access control, or regulatory demands require stronger boundaries.
- Performance threshold: when real metrics show the current design is no longer sufficient.
