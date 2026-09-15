# Lords Mobile Clone — Multi-Agent Build

This repo coordinates 13 AI agents building a Lords Mobile–style game
(React + Node.js + PostgreSQL). Each agent has its own folder under `agents/`
with a self-contained task brief you can hand to a separate AI coding session
running in this same project checkout (or a git worktree per agent, to avoid
file conflicts during parallel work).

## Run order

**Phase 0 (must run first, alone):**
- `agents/01-architect` — produces the shared spec in `docs/`. Everyone else
  depends on its output.

**Phase 1 (parallel, once docs/ exists):**
- `agents/02-database`
- `agents/03-auth`
- `agents/04-backend-core`
- `agents/07-frontend-ui` (can start against mocked API contracts)
- `agents/10-devops-qa` (Docker/CI scaffolding)

**Phase 2 (parallel, depends on Phase 1 backend scaffolding):**
- `agents/05-realtime`
- `agents/06-game-logic`
- `agents/09-alliance-social`
- `agents/11-payments`
- `agents/13-notifications`

**Phase 3 (once real APIs exist):**
- `agents/08-frontend-integration`
- `agents/12-admin-panel`

## Parallel-work rules (avoid collisions)

1. Each agent works **only** inside its assigned source path (listed in its
   own README's "Owns" section). Never edit another agent's owned paths.
2. Shared contracts live in `docs/` (`db-schema.md`, `api-contract.md`,
   `websocket-events.md`, `spec.md`). Agents **read** these but only
   `01-architect` (and, for schema, `02-database`) may **write** them —
   propose changes via a note in `docs/CHANGE-REQUESTS.md` instead of editing
   directly.
3. Use one git branch per agent (e.g. `agent/04-backend-core`) and merge via
   PR into `main` so conflicts surface early.
4. If two agents need the same shared file changed, that's a signal it should
   move into `docs/` as a contract instead of being duplicated.

## Folder layout

```
lords-mobile-ai-agents/
  README.md                 <- this file
  AGENTS_PLAN.md             <- original scoping rationale
  docs/                       <- shared contracts (spec, db schema, API, events)
  agents/
    01-architect/README.md
    02-database/README.md
    03-auth/README.md
    04-backend-core/README.md
    05-realtime/README.md
    06-game-logic/README.md
    07-frontend-ui/README.md
    08-frontend-integration/README.md
    09-alliance-social/README.md
    10-devops-qa/README.md
    11-payments/README.md
    12-admin-panel/README.md
    13-notifications/README.md
```

Each `agents/<n>/README.md` is written to be pasted as the opening prompt for
that agent's session — it states the goal, owned paths, inputs it depends on,
and deliverables.
