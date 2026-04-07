---
description: Coordinate multiple agents for complex tasks. Use for multi-perspective analysis, comprehensive reviews, or tasks requiring different domain expertise.
---

# Multi-Agent Orchestration

You are now in **ORCHESTRATION MODE**. Your task: coordinate specialized agents to solve this complex problem.

## Task to Orchestrate
$ARGUMENTS

---

## 🔴 CRITICAL: Minimum Agent Requirement

> Use as many agents as the task needs.
>
> Complex multi-domain work typically needs 3 or more agents.
>
> Do not pad orchestration with unnecessary agents just to meet a quota.

### Agent Selection Matrix

| Task Type | REQUIRED Agents (minimum) |
|-----------|---------------------------|
| **Web App** | frontend-specialist, backend-specialist, test-engineer |
| **API** | backend-specialist, security-auditor, test-engineer |
| **UI/Design** | frontend-specialist, performance-optimizer |
| **Database** | database-architect, backend-specialist |
| **Full Stack** | project-planner, frontend-specialist, backend-specialist |
| **Debug** | debugger, explorer-agent |
| **Security** | security-auditor, penetration-tester |

---

## Pre-Flight: Mode Check

This workflow should be usable from different agent hosts and editors, including VS Code-based environments and other agent runtimes. Treat mode names as conceptual states rather than product-specific features.

| Current Mode | Task Type | Action |
|--------------|-----------|--------|
| **plan** | Any | ✅ Proceed with planning-first approach |
| **edit** | Simple execution | ✅ Proceed directly |
| **edit** | Complex/multi-file | ⚠️ Ask: "This task requires planning. Switch to plan mode?" |
| **ask** | Any | ⚠️ Ask: "Ready to orchestrate. Switch to edit or plan mode?" |

---

## 🔴 STRICT 2-PHASE ORCHESTRATION

### PHASE 1: PLANNING (When Needed)

| Step | Agent | Action |
|------|-------|--------|
| 1 | `project-planner` | Create plan file when scope warrants it |
| 2 | (optional) `explorer-agent` | Codebase discovery if needed |

> Keep planning lightweight when the task is already clear.

### ⏸️ CHECKPOINT: User Approval

```
After a substantial plan is complete, ask for approval when the user asked for planning or when the plan introduces major product/architecture choices:

"✅ Plan created: ./<task-slug>.md

Do you approve? (Y/N)
- Y: Start implementation
- N: I'll revise the plan"
```

> For straightforward execution tasks, explicit plan approval is not required.

### PHASE 2: IMPLEMENTATION

| Parallel Group | Agents |
|----------------|--------|
| Foundation | `database-architect`, `security-auditor` |
| Core | `backend-specialist`, `frontend-specialist` |
| Polish | `test-engineer`, `devops-engineer` |

> Invoke multiple agents in parallel only when the workstreams are actually independent.

## Available Agents

| Agent | Domain | Use When |
|-------|--------|----------|
| `project-planner` | Planning | Task breakdown, plan file |
| `explorer-agent` | Discovery | Codebase mapping |
| `frontend-specialist` | UI/UX | React, Vue, CSS, HTML |
| `backend-specialist` | Server | API, Node.js, Python |
| `database-architect` | Data | SQL, NoSQL, Schema |
| `security-auditor` | Security | Vulnerabilities, Auth |
| `penetration-tester` | Security | Active testing |
| `test-engineer` | Testing | Unit, E2E, Coverage |
| `devops-engineer` | Ops | CI/CD, Docker, Deploy |
| `mobile-developer` | Mobile | React Native, Flutter |
| `performance-optimizer` | Speed | Lighthouse, Profiling |
| `seo-specialist` | SEO | Meta, Schema, Rankings |
| `documentation-writer` | Docs | README, API docs |
| `debugger` | Debug | Error analysis |
| `game-developer` | Games | Unity, Godot |
| `orchestrator` | Meta | Coordination |

---

## Orchestration Protocol

### Step 1: Analyze Task Domains
Identify ALL domains this task touches:
```
□ Security     → security-auditor, penetration-tester
□ Backend/API  → backend-specialist
□ Frontend/UI  → frontend-specialist
□ Database     → database-architect
□ Testing      → test-engineer
□ DevOps       → devops-engineer
□ Mobile       → mobile-developer
□ Performance  → performance-optimizer
□ SEO          → seo-specialist
□ Planning     → project-planner
```

### Step 2: Phase Detection

| If Plan Exists | Action |
|----------------|--------|
| NO plan file | → Go to PHASE 1 only if the task is large or ambiguous |
| Plan exists or task is already clear | → Go to PHASE 2 |

### Step 3: Execute Based on Phase

**PHASE 1 (Planning):**
```
Use the project-planner agent to create `./{task-slug}.md`
→ Stop after plan is created only if approval is needed
→ Otherwise continue to implementation
```

**PHASE 2 (Implementation - after approval):**
```
Invoke agents in PARALLEL:
Use the frontend-specialist agent to [task]
Use the backend-specialist agent to [task]
Use the test-engineer agent to [task]
```

**🔴 CRITICAL: Context Passing (MANDATORY)**

When invoking ANY subagent, you MUST include:

1. **Original User Request:** Full text of what user asked
2. **Decisions Made:** All user answers to Socratic questions
3. **Previous Agent Work:** Summary of what previous agents did
4. **Current Plan State:** If plan files exist in workspace, include them

**Example with FULL context:**
```
Use the project-planner agent to create `./{task-slug}.md`:

**CONTEXT:**
- User Request: "A social platform for students, using mock data"
- Decisions: Tech=Vue 3, Layout=Grid Widgets, Auth=Mock, Design=Youthful & dynamic
- Previous Work: Orchestrator asked 6 questions, user chose all options
- Current Plan: playful-roaming-dream.md exists in workspace with initial structure

**TASK:** Create a detailed plan file based on the decisions above. Use dynamic naming in project root. Do NOT infer from folder name.
```

> ⚠️ **VIOLATION:** Invoking subagent without full context = subagent will make wrong assumptions!


### Step 4: Verification (MANDATORY)
Prefer the master validation scripts documented in `ARCHITECTURE.md`, then add targeted skill-level scripts only when they materially improve confidence for the task. Use the active local app URL when known; otherwise substitute the correct preview/dev URL for the current environment:
```bash
python .agent/scripts/checklist.py .

# For release-grade or high-risk changes, run the full suite
python .agent/scripts/verify_all.py . --url <local-app-url>
```

Examples of targeted add-on checks when relevant:

```bash
python .agent/skills/vulnerability-scanner/scripts/security_scan.py .
python .agent/skills/lint-and-validate/scripts/lint_runner.py .
python .agent/skills/testing-patterns/scripts/test_runner.py .
```

### Step 5: Synthesize Results
Combine all agent outputs into unified report.

---

## Output Format

```markdown
## 🎼 Orchestration Report

### Task
[Original task summary]

### Mode
[Current agent mode/state: plan/edit/ask or equivalent host concept]

### Agents Invoked
| # | Agent | Focus Area | Status |
|---|-------|------------|--------|
| 1 | project-planner | Task breakdown | ✅ |
| 2 | frontend-specialist | UI implementation | ✅ |
| 3 | test-engineer | Verification scripts | ✅ |

### Verification Scripts Executed
- [x] checklist.py → Pass/Fail
- [x] verify_all.py → Pass/Fail/Skipped
- [x] targeted skill checks (if any) → Pass/Fail/Skipped

### Key Findings
1. **[Agent 1]**: Finding
2. **[Agent 2]**: Finding
3. **[Agent 3]**: Finding

### Deliverables
- [ ] Plan file created when planning was needed
- [ ] Code implemented
- [ ] Tests passing
- [ ] Scripts verified

### Summary
[One paragraph synthesis of all agent work]
```

---

## 🔴 EXIT GATE

Before completing orchestration, verify:

1. ✅ **Agent Selection:** Agents used match the task domains
2. ✅ **Scripts Executed:** `checklist.py` or equivalent relevant verification ran for the affected areas
3. ✅ **Report Generated:** Orchestration Report with all agents listed

> **If any check fails → do not mark orchestration complete. Re-route, verify, or continue execution.**

---

**Begin orchestration now. Select the right agents, execute in a sensible order, run relevant verification, and synthesize results.**
