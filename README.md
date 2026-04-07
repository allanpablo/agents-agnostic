# agents-agnostic

Portable, host-agnostic AI agent kit for orchestrators, specialists, workflows, and validation across IDEs, CLIs, and chat platforms.

[PT-BR](#pt-br) | [English](#english)

---

## PT-BR

### O que e

`agents-agnostic` e um kit portavel de agentes para uso em diferentes plataformas de IA, IDEs e CLIs.

A ideia central e simples:
- manter agentes, skills, workflows e regras dentro do repositorio
- versionar tudo junto com o projeto
- reutilizar o mesmo modelo operacional em diferentes runtimes
- mudar apenas a forma de invocacao conforme a plataforma

### Estrutura

```text
.agent/
├── ARCHITECTURE.md
├── USAGE.md
├── agents/
├── skills/
├── workflows/
├── rules/
├── operator-profile/
└── scripts/
```

### O que o projeto entrega

- `20` agentes especialistas
- `53` skills
- `11` workflows
- convencao de planejamento e orquestracao
- scripts de validacao para checklist e verificacao completa

### Componentes principais

#### Agentes

Exemplos:
- `orchestrator`
- `project-planner`
- `backend-specialist`
- `frontend-specialist`
- `security-auditor`
- `test-engineer`
- `debugger`
- `devops-engineer`

#### Skills

Exemplos:
- `parallel-agents`
- `plan-writing`
- `brainstorming`
- `lint-and-validate`
- `vulnerability-scanner`
- `testing-patterns`
- `frontend-design`
- `api-patterns`

#### Workflows

- `/plan`
- `/orchestrate`
- `/create`
- `/enhance`
- `/debug`
- `/test`
- `/deploy`
- `/preview`
- `/status`
- `/brainstorm`
- `/ui-ux-pro-max`

### Por que "agents-agnostic"

Porque o kit nao depende de um unico fornecedor de IA, editor ou CLI.

Ele foi pensado para funcionar em:
- IDEs com assistente de IA
- runtimes de agentes via terminal
- plataformas de chat com contexto de projeto
- copilotos internos baseados em API

O que permanece igual:
- a pasta `.agent/`
- os nomes dos agentes
- os nomes dos workflows
- a convencao de plano
- os pontos de entrada de validacao

O que muda e apenas a sintaxe de invocacao em cada ambiente.

### Convencao de planejamento

Os planos sao dinamicos e ficam na raiz do projeto:

```text
./{task-slug}.md
```

Exemplos:
- `./saas-dashboard.md`
- `./auth-refactor.md`
- `./fitness-app.md`

Nao use nomes fixos como:
- `PLAN.md`
- `docs/PLAN.md`

### Validacao

Validacao principal:

```bash
python .agent/scripts/checklist.py .
```

Verificacao completa:

```bash
python .agent/scripts/verify_all.py . --url <local-app-url>
```

Checks direcionados opcionais:

```bash
python .agent/skills/vulnerability-scanner/scripts/security_scan.py .
python .agent/skills/lint-and-validate/scripts/lint_runner.py .
python .agent/skills/testing-patterns/scripts/test_runner.py .
```

### Como usar

#### Em IDEs

Exemplos de prompt:

```text
Read .agent/ARCHITECTURE.md and use the orchestrator agent for this task: implement RBAC and audit logs.
```

```text
Follow .agent/workflows/plan.md for this task: create a clinic scheduling platform.
```

#### Em CLIs

Se a CLI suportar slash commands:

```text
/plan build a multi-tenant CRM
/orchestrate review auth, fix backend issues, and add tests
```

Se a CLI nao suportar slash commands:

```text
Follow .agent/workflows/orchestrate.md for this task: review auth, fix backend issues, and add tests.
```

#### Em plataformas de chat

Exemplo de prompt:

```text
Use the local .agent rules and orchestrator. Start by reading .agent/ARCHITECTURE.md.
```

### Quick Start

#### 1. Coloque a pasta `.agent/` no repositorio

#### 2. Abra o projeto no ambiente de IA de sua escolha

#### 3. Comece por:

```text
Read .agent/ARCHITECTURE.md first.
```

#### 4. Escolha o modo de execucao

Planejamento:

```text
Follow .agent/workflows/plan.md for this task: <task>
```

Orquestracao:

```text
Follow .agent/workflows/orchestrate.md for this task: <task>
```

Execucao direta com especialista:

```text
Use .agent/agents/backend-specialist.md for this task: <task>
```

### Documentacao

- arquitetura: `.agent/ARCHITECTURE.md`
- guia de uso: `.agent/USAGE.md`
- agentes: `.agent/agents/`
- workflows: `.agent/workflows/`
- skills: `.agent/skills/`

### Status

Este repositorio foi estruturado como uma camada portavel de agentes.

Ele foi desenhado para:
- evitar acoplamento forte com um unico host
- manter workflows legiveis em markdown
- permitir evolucao dos agentes via versionamento

### Licenca

Adicione a licenca de sua escolha antes de publicar.

---

## English

### What It Is

`agents-agnostic` is a portable agent kit designed to work across different AI platforms, IDEs, and CLIs.

The core idea is simple:
- keep agents, skills, workflows, and rules inside the repository
- version everything together with the project
- reuse the same operating model across different runtimes
- only change the invocation style for each platform

### Structure

```text
.agent/
├── ARCHITECTURE.md
├── USAGE.md
├── agents/
├── skills/
├── workflows/
├── rules/
├── operator-profile/
└── scripts/
```

### What You Get

- `20` specialist agents
- `53` skills
- `11` workflows
- planning and orchestration conventions
- validation scripts for checklist and full verification

### Main Components

#### Agents

Examples:
- `orchestrator`
- `project-planner`
- `backend-specialist`
- `frontend-specialist`
- `security-auditor`
- `test-engineer`
- `debugger`
- `devops-engineer`

#### Skills

Examples:
- `parallel-agents`
- `plan-writing`
- `brainstorming`
- `lint-and-validate`
- `vulnerability-scanner`
- `testing-patterns`
- `frontend-design`
- `api-patterns`

#### Workflows

- `/plan`
- `/orchestrate`
- `/create`
- `/enhance`
- `/debug`
- `/test`
- `/deploy`
- `/preview`
- `/status`
- `/brainstorm`
- `/ui-ux-pro-max`

### Why "agents-agnostic"

Because the kit does not depend on a single AI vendor, editor, or CLI.

It is designed to work across:
- AI coding IDEs
- terminal agent runtimes
- chat platforms with project context
- internal API-driven copilots

What stays the same:
- the `.agent/` folder
- the agent names
- the workflow names
- the planning convention
- the validation entrypoints

What changes is only the invocation syntax per environment.

### Planning Convention

Plans are dynamic and stored at project root:

```text
./{task-slug}.md
```

Examples:
- `./saas-dashboard.md`
- `./auth-refactor.md`
- `./fitness-app.md`

Do not use fixed names such as:
- `PLAN.md`
- `docs/PLAN.md`

### Validation

Core validation:

```bash
python .agent/scripts/checklist.py .
```

Full verification:

```bash
python .agent/scripts/verify_all.py . --url <local-app-url>
```

Optional targeted checks:

```bash
python .agent/skills/vulnerability-scanner/scripts/security_scan.py .
python .agent/skills/lint-and-validate/scripts/lint_runner.py .
python .agent/skills/testing-patterns/scripts/test_runner.py .
```

### How To Use

#### In IDEs

Prompt examples:

```text
Read .agent/ARCHITECTURE.md and use the orchestrator agent for this task: implement RBAC and audit logs.
```

```text
Follow .agent/workflows/plan.md for this task: create a clinic scheduling platform.
```

#### In CLIs

If the CLI supports slash commands:

```text
/plan build a multi-tenant CRM
/orchestrate review auth, fix backend issues, and add tests
```

If the CLI does not support slash commands:

```text
Follow .agent/workflows/orchestrate.md for this task: review auth, fix backend issues, and add tests.
```

#### In Chat Platforms

Prompt example:

```text
Use the local .agent rules and orchestrator. Start by reading .agent/ARCHITECTURE.md.
```

### Quick Start

#### 1. Put the `.agent/` folder in your repository

#### 2. Open the project in your AI environment of choice

#### 3. Start with:

```text
Read .agent/ARCHITECTURE.md first.
```

#### 4. Choose an execution style

Planning:

```text
Follow .agent/workflows/plan.md for this task: <task>
```

Orchestration:

```text
Follow .agent/workflows/orchestrate.md for this task: <task>
```

Direct specialist execution:

```text
Use .agent/agents/backend-specialist.md for this task: <task>
```

### Documentation

- architecture: `.agent/ARCHITECTURE.md`
- usage guide: `.agent/USAGE.md`
- agents: `.agent/agents/`
- workflows: `.agent/workflows/`
- skills: `.agent/skills/`

### Status

This repository is structured as a portable agent layer.

It is designed to:
- avoid hard-coupling to a single host
- keep workflows readable as markdown
- let teams evolve agents through version control

### License

Add the license of your choice before publishing.
