# Agent 09 — Alliance & Social

## Depends on
`02-database` schema, `03-auth`, `04-backend-core`, `05-realtime` (for alliance chat).

## Owns
- `/backend/src/modules/alliance/`
- `/backend/src/modules/leaderboards/`
- `/backend/src/modules/friends/`

## Goal
Alliance/guild system, alliance wars, territory on the world map, friend
lists, and leaderboards.

## Deliverables
1. Alliance CRUD: create, join/leave/kick, roles (leader/officer/member) and
   permissions.
2. Alliance war: declare war, contribution tracking, war score, rewards.
3. Territory/kingdom map ownership tied into the world map (coordinate with
   `06-game-logic`'s PvE/map nodes via `docs/api-contract.md`).
4. Leaderboards: power ranking, kill count, alliance ranking — efficient
   queries (materialized view or scheduled recompute; document choice).
5. Friend list: add/remove/block, friend gifting stub.
6. Alliance chat channel wiring with `05-realtime` (reuse its chat module,
   just scope a channel per alliance).

## Constraints
- Reuse `05-realtime`'s chat infrastructure — don't build a second chat system.
- Don't touch city/troop/building logic — only alliance-scoped data.

## Definition of done
Two test players can create an alliance, one can join, both see each other
in an alliance chat channel, and a leaderboard query returns ranked results.
