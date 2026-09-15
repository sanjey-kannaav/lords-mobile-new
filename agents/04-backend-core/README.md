# Agent 04 — Backend Core

## Depends on
`docs/api-contract.md`, `02-database` schema, `03-auth` middleware.

## Owns
- `/backend/src/modules/player/`
- `/backend/src/modules/city/`
- `/backend/src/modules/buildings/`
- `/backend/src/modules/troops/`
- `/backend/src/modules/inventory/`
- `/backend/src/jobs/` (timers/queues for build & train completion)

## Goal
Core game state API: player profile, city/base, building construction &
upgrades with timers, resource production ticking, troop training queues,
inventory management.

## Deliverables
1. Endpoints per `docs/api-contract.md` for: player profile, city state,
   building list/upgrade/collect, troop training queue, inventory.
2. Resource production engine — ticks resource generation based on building
   levels (cron job or lazy-calc-on-read pattern; document which you chose).
3. Timer/queue system for building upgrades and troop training (e.g.
   BullMQ + Redis, or DB-based timestamp checks) — expose ETA to frontend.
4. Idempotent "collect resources" and "complete queue item" endpoints.
5. Integration tests covering a full loop: create city → start build →
   fast-forward timer → collect → verify resource balance.

## Constraints
- Do not implement combat, heroes, or gacha — that's `06-game-logic`.
- Do not implement chat/websockets — that's `05-realtime`.
- Use only the DB schema/migrations from `02-database`; if a field is
  missing, file it in `docs/CHANGE-REQUESTS.md` rather than editing the
  schema yourself.

## Definition of done
A player can register (via auth), fetch their city, queue a building upgrade,
have it complete after its timer, and see resources accrue — all via API
calls, with tests proving it.
