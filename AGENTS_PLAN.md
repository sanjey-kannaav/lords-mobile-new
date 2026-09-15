# Lords Mobile Clone — AI Agent Team Plan

Building a full "Lords Mobile"-style game (kingdom building, hero collection, troop
training, PvP/PvE combat, alliances, real-time chat, guild wars, gacha/summon
system, map exploration) with **React (frontend) + Node.js (backend) + PostgreSQL
(database)** is a large multi-domain project. Realistically this is equivalent to
a small studio's work (6-12 months for a real team). Below is the recommended
breakdown into **AI agents**, each scoped to a domain so a single agent's context
doesn't get overloaded and work can proceed in parallel.

## Recommended: 10 agents

| # | Agent | Responsibility |
|---|-------|-----------------|
| 1 | **architect-agent** | Overall system design: repo structure, API contracts, DB schema, tech stack decisions, coding conventions. Produces the spec other agents build against. |
| 2 | **database-agent** | PostgreSQL schema design & migrations (users, resources, buildings, troops, heroes, items, alliances, battles, leaderboards). ORM setup (Prisma/Sequelize/TypeORM). |
| 3 | **auth-agent** | User accounts, JWT/session auth, registration/login, password reset, OAuth (Google/Facebook login), rate limiting, security hardening. |
| 4 | **backend-core-agent** | Node.js/Express (or NestJS) REST/GraphQL API: player state, resource production, building upgrades, troop training queues, inventory, timers. |
| 5 | **realtime-agent** | WebSocket/Socket.io layer: live chat, alliance chat, notifications, live troop movement, battle results push, presence. |
| 6 | **game-logic-agent** | Core game rules engine: combat resolution/formulas, hero stats & leveling, gacha/summon probability system, resource/production balancing, PvE (monster hunting), quests. |
| 7 | **frontend-ui-agent** | React app: game dashboard, city-building UI, hero screens, map view, inventory, shop, animations, responsive layout, state management (Redux/Zustand). |
| 8 | **frontend-integration-agent** | Wires React frontend to backend APIs/WebSockets, handles auth flows, caching (React Query), error/loading states, real-time UI updates. |
| 9 | **alliance-social-agent** | Alliance/guild system: creation, roles/permissions, alliance wars, territory/kingdom map, leaderboards, friend system. |
| 10 | **devops-qa-agent** | Docker Compose setup (Node + Postgres + Redis), CI/CD, environment configs, automated tests (unit/integration/e2e), load testing, deployment scripts. |

### Optional / scale-up agents (if you want more granularity)
- **payments-agent** — in-app purchases, virtual currency, store/receipt validation.
- **admin-panel-agent** — internal dashboard for game masters (ban players, adjust economy, push events).
- **notifications-agent** — push notifications, email digests, scheduled events/cron jobs.

## How to run this
Each row above should become a separate agent session/task, working from the
shared spec produced by `architect-agent`. Suggested order:

1. `architect-agent` runs first and produces `/docs/spec.md`, `/docs/db-schema.md`, `/docs/api-contract.md`.
2. `database-agent`, `auth-agent`, `backend-core-agent` can run in parallel once the spec exists.
3. `game-logic-agent` and `realtime-agent` build on top of `backend-core-agent`'s scaffolding.
4. `frontend-ui-agent` can start in parallel with backend work using mocked API contracts.
5. `frontend-integration-agent` runs once real APIs are ready.
6. `alliance-social-agent` and `devops-qa-agent` run continuously alongside/after the above.

## Notes
- 10 agents is the practical sweet spot: fewer than that and single agents get
  overloaded with unrelated domains (bad for context and quality); more than
  that adds coordination overhead without much benefit for a project this size.
- All agents should read/write to the shared `/docs` spec files so they stay in sync.
- This is a genuinely large build — expect this to be an iterative, multi-session
  effort, not a single run.
