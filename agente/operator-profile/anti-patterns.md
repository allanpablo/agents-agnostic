# Anti-Patterns

These are patterns the system should avoid unless there is a clear justification.

## Default Anti-Patterns
- Premature abstraction
- Enterprise patterns without enterprise constraints
- Generic UI with no product point of view
- Excessive indirection
- Unnecessary microservices
- Tight coupling between layers
- Fragile tests with low signal
- Overuse of global state
- Heavy dependencies for small problems
- Hidden magic and implicit behavior

## Your Personal Anti-Patterns

### Overengineering
- Why it is bad: increases delivery cost, operational burden, and maintenance without real benefit.
- What to do instead: start with a modular and observable foundation.
- Exception cases: compliance, scale, or reliability constraints already proven.

### Systems without integration
- Why it is bad: creates silos, duplicate work, and fragile manual operations.
- What to do instead: prefer API, webhook, HL7, FHIR, or ETL integration paths.
- Exception cases: isolated proof-of-concept with short lifespan.

### Spreadsheets as the core system
- Why it is bad: weak governance, hard auditing, and business logic leakage.
- What to do instead: use spreadsheets as operational support, not system of record.
- Exception cases: lightweight tracking while the real product capability is being built.

### Missing logging or audit trail
- Why it is bad: breaks troubleshooting, accountability, and trust.
- What to do instead: add structured logs and auditable events at key flows.
- Exception cases: throwaway prototypes with no operational use.

### Hardcoded critical business rules
- Why it is bad: makes evolution risky and hides domain behavior.
- What to do instead: move critical rules into explicit domain logic and configuration where appropriate.
- Exception cases: narrow transitional code with a clear near-term refactor path.

### Manual deploy without versioning
- Why it is bad: weak rollback, weak traceability, and incident amplification.
- What to do instead: versioned deploys with simple Docker-based release flow.
- Exception cases: none for production.

### External integrations without fallback
- Why it is bad: couples uptime and correctness to third-party behavior.
- What to do instead: retries, buffering, alerts, and manual fallback paths when needed.
- Exception cases: low-risk internal integrations with negligible impact.

### IA without control
- Why it is bad: produces inconsistent, unauditable, and unsafe outputs.
- What to do instead: constrain prompts, validate outputs, define guardrails, and add fallback behavior.
- Exception cases: internal experimentation clearly isolated from production.

### Beautiful UI that does not solve operations
- Why it is bad: looks good but fails the actual workflow.
- What to do instead: optimize for throughput, clarity, and operational correctness first.
- Exception cases: marketing pages where perception is the primary goal.

### Automating a broken process
- Why it is bad: scales waste and confusion.
- What to do instead: simplify and redesign the workflow before automating it.
- Exception cases: temporary automation to absorb urgent operational load.

## Smells That Should Trigger Review
- New abstraction with only one call site
- Async workflow without failure visibility
- New dependency that replaces simple platform capability
- Config complexity larger than feature complexity
- New model/provider added without evaluation criteria
- Tenant-sensitive flow without auditability
- Healthcare integration without clear contract and fallback
