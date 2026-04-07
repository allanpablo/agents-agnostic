# Agent Kit Usage Guide

This document explains how to use your agents, skills, and orchestrators across current AI platforms, IDEs, and CLIs.

## Goal

This kit was organized to work as a portable `.agent` workspace layer.

It gives you:
- specialist agents for domain work
- orchestrators for multi-agent execution
- reusable skills
- slash-style workflows
- validation scripts

The operational model is host-neutral:
- use the host runtime to load or reference files from `.agent/`
- use the same agent names, workflow names, and plan conventions everywhere possible
- adapt only the invocation style to the platform you are using

## Folder Contract

Your workspace contract is:

```text
.agent/
  agents/
  skills/
  workflows/
  rules/
  operator-profile/
  scripts/
```

Key conventions:
- planning file: `./{task-slug}.md`
- orchestration workflow: `/orchestrate`
- planning workflow: `/plan`
- core validation: `python .agent/scripts/checklist.py .`
- full validation: `python .agent/scripts/verify_all.py . --url <local-app-url>`

## Core Operating Model

Use the kit in 4 layers:

1. `rules/`
Global behavior and execution rules.

2. `agents/`
Specialist personas like `backend-specialist`, `frontend-specialist`, `security-auditor`, `project-planner`, and `orchestrator`.

3. `skills/`
Targeted knowledge packs loaded on demand.

4. `workflows/`
Reusable command patterns like `/plan`, `/orchestrate`, `/debug`, `/deploy`.

## Recommended Usage by Environment

## 1. AI Coding IDEs

Examples:
- VS Code with agent extensions
- Cursor-style editors
- Windsurf-style editors
- editor-integrated Claude/Gemini/OpenAI tooling

Best way to use:
- open the repo root so `.agent/` is visible to the assistant
- instruct the assistant to read `.agent/ARCHITECTURE.md` first
- then tell it which agent or workflow to follow

Good prompts:

```text
Read .agent/ARCHITECTURE.md and use the orchestrator agent for this task: build multi-tenant auth for my SaaS.
```

```text
Follow .agent/workflows/plan.md for: create a clinic scheduling dashboard.
```

```text
Use .agent/agents/backend-specialist.md and only work on the API layer.
```

Practical pattern:
- simple fix: call one specialist agent
- medium feature: use `project-planner` then specialist agents
- complex feature: use `orchestrator`

## 2. CLI Agent Runtimes

Examples:
- Claude Code style CLI
- OpenAI/Codex style CLI
- Gemini CLI style workflows
- custom terminal agent wrappers

Best way to use:
- run from the project root
- keep `.agent/` inside the same workspace
- reference workflow files explicitly in the prompt if slash commands are not native

If the CLI supports slash commands:

```text
/plan build a healthcare intake system
/orchestrate review auth, audit security, and add missing tests
/debug investigate why the webhook retries forever
```

If the CLI does not support slash commands natively:

```text
Follow the workflow in .agent/workflows/orchestrate.md for this task: review the billing module, fix backend issues, and add tests.
```

```text
Follow .agent/workflows/plan.md and create a plan for a mobile fitness app.
```

## 3. Chat Platforms With File/Project Context

Examples:
- ChatGPT Projects
- Claude Projects
- Gemini Advanced with workspace context

Best way to use:
- attach or sync the repository
- ensure `.agent/` is included in project context
- explicitly ask the model to honor the local agent files

Good prompts:

```text
Use the local .agent rules and orchestrator. Start by reading .agent/ARCHITECTURE.md, then coordinate the right agents for implementing audit logs and RBAC.
```

```text
Use the project-planner agent from .agent/agents/project-planner.md and create ./{task-slug}.md for a CRM pipeline feature.
```

Important limitation:
- chat platforms vary in how reliably they preserve long local instructions
- for longer tasks, restate the target agent/workflow in each new session or major turn

## 4. API-Driven Custom Platforms

Examples:
- internal copilots
- MCP-based shells
- custom orchestration services
- team portals that invoke models through API

Best way to use:
- treat `.agent/` as the instruction layer mounted with every task
- inject these files in priority order:

```text
1. .agent/rules/GEMINI.md
2. selected file from .agent/agents/
3. selected files from .agent/skills/
4. selected file from .agent/workflows/
```

Recommended policy:
- always preload `.agent/ARCHITECTURE.md`
- then select one primary agent
- then load only the skills referenced by that agent
- load a workflow file only when using workflow-style execution

## How To Choose Between Specialist, Planner, and Orchestrator

Use a specialist agent when:
- the task is single-domain
- the change is scoped to one layer
- you already know what needs to be done

Examples:
- `backend-specialist` for API changes
- `frontend-specialist` for UI work
- `debugger` for root-cause analysis
- `security-auditor` for auth and risk review

Use `project-planner` when:
- the task is large
- the task is ambiguous
- you want a task graph before coding
- multiple files or systems will change

Output convention:
- `./{task-slug}.md`

Use `orchestrator` when:
- the task spans multiple domains
- you need coordination between agents
- you want parallel analysis or implementation streams
- the task includes security, backend, frontend, tests, and ops concerns together

## Supported Workflow Style

The canonical workflows are:
- `/brainstorm`
- `/plan`
- `/create`
- `/enhance`
- `/debug`
- `/test`
- `/deploy`
- `/preview`
- `/status`
- `/orchestrate`
- `/ui-ux-pro-max`

If your platform does not support slash commands, use this translation:

```text
Follow .agent/workflows/<workflow>.md for this task: <your request>
```

Examples:

```text
Follow .agent/workflows/debug.md for this task: API returns 500 on tenant creation.
```

```text
Follow .agent/workflows/test.md for this task: validate the checkout flow.
```

## Planning Convention

Planning is dynamic and root-based.

Use:
- `./saas-dashboard.md`
- `./auth-refactor.md`
- `./fitness-app.md`

Do not use:
- `PLAN.md`
- `docs/PLAN.md`
- generic fixed plan names

Use planning when:
- the task is structurally large
- architecture decisions matter
- you need approvals before implementation

Skip mandatory planning when:
- the task is clear and bounded
- the change is small enough to execute directly

## Orchestration Convention

The `orchestrator` should:
- detect OS, shell, package manager, and runtime context
- ask only the minimum clarifying questions
- use a plan file only when the task needs one
- route work to the correct specialist agents
- preserve agent boundaries
- run relevant verification

Typical orchestration flow:

```text
1. Read context and existing plan files
2. Decide if planning is needed
3. Select the right agents
4. Run independent work in parallel when safe
5. Run tests and verification
6. Synthesize a unified report
```

## Validation and Runtime Checks

Recommended validation entrypoints:

```bash
python .agent/scripts/checklist.py .
python .agent/scripts/verify_all.py . --url <local-app-url>
```

Use targeted checks only when needed:

```bash
python .agent/skills/vulnerability-scanner/scripts/security_scan.py .
python .agent/skills/lint-and-validate/scripts/lint_runner.py .
python .agent/skills/testing-patterns/scripts/test_runner.py .
```

## IDE and CLI Prompt Templates

## Single specialist

```text
Read .agent/ARCHITECTURE.md, then use .agent/agents/backend-specialist.md for this task: add tenant-scoped invoice endpoints.
```

## Planning first

```text
Read .agent/ARCHITECTURE.md and follow .agent/workflows/plan.md for this task: build a patient triage dashboard.
```

## Full orchestration

```text
Read .agent/ARCHITECTURE.md, then use the orchestrator agent to handle this multi-domain task: review our auth flow, fix backend issues, add tests, and validate security.
```

## Debug flow

```text
Follow .agent/workflows/debug.md for this issue: webhook processing duplicates messages under retry.
```

## Team Usage Model

For solo use:
- call agents directly from prompts
- use `/plan` and `/orchestrate` as your main control points

For team use:
- keep `.agent/` versioned in the repo
- standardize plan naming in root
- require verification commands before task closure
- document which workflows the team uses most

## Portability Rules

To keep the kit portable across platforms:
- keep `.agent/` at repo root
- avoid host-specific assumptions in prompts
- reference files explicitly when slash commands are unavailable
- prefer placeholders like `<local-app-url>` over fixed localhost values
- let the runtime detect OS and shell before emitting commands

## Practical Recommendation

If the platform is mature and has good workspace context:
- use `orchestrator` as the default entry for complex work

If the platform is weak at long context retention:
- explicitly name the workflow and the primary agent in every major prompt

If the platform is CLI-first:
- keep usage centered on `.agent/workflows/*.md`
- run validation scripts from terminal after implementation

## Minimal Starter Commands

Use these as your default operating set:

```text
/plan <task>
/orchestrate <task>
/debug <issue>
/test <scope>
```

Or, in platforms without slash commands:

```text
Follow .agent/workflows/plan.md for this task: <task>
Follow .agent/workflows/orchestrate.md for this task: <task>
Follow .agent/workflows/debug.md for this issue: <issue>
Follow .agent/workflows/test.md for this scope: <scope>
```

## Final Rule

Across IDE, CLI, chat, or API environments, keep this invariant:

- same `.agent/` folder
- same agent names
- same workflow names
- same plan-file convention
- same validation entrypoints

Only the invocation syntax should change between platforms.
