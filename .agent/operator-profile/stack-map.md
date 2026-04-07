# Stack Map

## Languages
- Primary: TypeScript
- Secondary: JavaScript, SQL, Python
- Notes: Python is mainly for automation, IA, and scripts.

## Frontend
- Frameworks: React, Next.js
- UI libraries: custom componentization with clean product-oriented patterns
- Styling: TailwindCSS
- Design preference: Vercel/Linear-inspired, clean and functional
- State management: prefer lightweight local patterns unless complexity justifies more
- Forms: choose pragmatic libraries based on project needs

## Backend
- Frameworks: Node.js with Fastify as preferred default
- API style: REST first, Webhooks when needed
- Architecture: modular services + domain + adapters
- ORM / access: Prisma preferred for product code
- Integration profile: strong support for healthcare and legacy integrations

## Data
- Primary database: PostgreSQL
- Secondary database: SQL Server for legacy and clinical integrations
- Cache / queue / events: Redis
- Data priority: structured, interoperable, and auditable data over presentation-first data handling

## Infra
- Containers: Docker, Docker Compose
- Orchestration: Coolify when simplified operations are preferable
- Hosting: VPS-first (Hostinger, Contabo)
- Virtualization / lab: Proxmox
- Networking: WireGuard, OpenVPN, pfSense
- Infra style: pragmatic, low-ceremony, operationally clear

## Observability
- Logs: centralized application + system logs
- Monitoring: uptime and critical service checks first
- Dashboards: simple dashboards, lightweight Grafana or operational sheets when enough
- Alerts: pragmatic alerts with low noise

## AI Stack
- Primary provider: OpenAI
- Fallback / multi-model: OpenRouter
- Secondary providers: Gemini, Claude
- Automation layer: n8n AI nodes
- Retrieval: simple RAG only when it adds clear value
- Agent goal: practical orchestration over experimental complexity

## Tooling
- Automation: n8n
- Support / operations: Chatwoot, Google Sheets
- Analytics / BI: Power BI when needed
- Dev tools: GitHub, VSCode, Postman, Insomnia

## Deploy / CI-CD
- Deploy style: Docker-based deploy
- Versioning: Git
- Delivery model: simple continuous deploy, no unnecessary pipeline complexity
- Rollback: fast manual rollback is preferred over elaborate release ceremony

## Non-Negotiables
- Prefer Node + PostgreSQL + Docker as the default delivery stack
- Keep deployment and rollback simple
- Design for integration with existing systems
- Favor operational clarity over platform complexity
