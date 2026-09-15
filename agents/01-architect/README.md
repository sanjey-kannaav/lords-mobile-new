# Agent 01 — Architect

## Goal
Define the overall system so all other agents can work in parallel without
colliding. Runs first, alone. No other agent should start until this is done.

## Owns
- `/docs/spec.md`
- `/docs/db-schema.md`
- `/docs/api-contract.md`
- `/docs/websocket-events.md`
- Top-level repo scaffolding: `/backend`, `/frontend`, `/shared`, `package.json` workspaces, `tsconfig.json`, lint/format configs.

## Deliverables
1. **`docs/spec.md`** — game feature list scoped for v1 (kingdom/city building,
   resource production, troop training, hero collection & leveling, gacha
   summon, PvE monster hunting, PvP battles, alliances/guilds, alliance wars,
   chat, leaderboards, map/world view). Mark v1 vs later-phase features.
2. **`docs/db-schema.md`** — entity list and relationships (users, players,
   cities, buildings, resources, troops, heroes, hero_instances, items,
   inventory, alliances, alliance_members, battles, battle_logs, quests,
   leaderboards, transactions). Include primary/foreign keys and key indexes.
3. **`docs/api-contract.md`** — REST/GraphQL endpoint list with request/response
   shapes for every domain (auth, player, city, troops, heroes, battle,
   alliance, shop). Versioned under `/api/v1`.
4. **`docs/websocket-events.md`** — event names and payloads for realtime
   features (chat message, troop movement, battle result, notification,
   alliance event).
5. **Repo scaffolding** — monorepo layout:
   ```
   /backend   (Node.js/TypeScript, Express or NestJS)
   /frontend  (React + TypeScript + Vite)
   /shared    (shared TS types generated from api-contract.md)
   /docs
   ```
   Pick and document: NestJS vs Express, Prisma vs TypeORM, Redux vs Zustand,
   Socket.io vs raw WS, Docker Compose for local Postgres/Redis.

## Constraints
- Keep v1 scope realistic — do not design for scale you don't need yet.
- Every decision must be written down in `docs/spec.md` with a one-line reason.
- Do not write feature implementation code — only scaffolding, configs, and docs.

## Definition of done
All four `docs/*.md` files exist and are internally consistent (schema fields
match API contract field names match websocket payload names), and the repo
builds (empty backend/frontend apps boot) via `docker compose up`.

## Shared status board (read this too)
Before you finish this session, update your row in the shared status board so
other agents/terminals know your progress:

```bash
cd /home/sanjey/Pictures/Script/clean_pages/lords-mobile-worktrees/planning
git pull origin dont-merge
# edit docs/STATUS.md — update only your own row
git add docs/STATUS.md && git commit -m "status: update" && git push origin dont-merge
```

Also check `docs/CHANGE-REQUESTS.md` there for any asks directed at you from
other agents, and log any of your own asks there instead of editing another
agent's owned files or the shared contract docs directly.
