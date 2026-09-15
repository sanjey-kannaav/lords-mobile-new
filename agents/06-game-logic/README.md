# Agent 06 — Game Logic

## Depends on
`docs/spec.md`, `02-database` schema, `04-backend-core` player/city/troops APIs.

## Owns
- `/backend/src/modules/heroes/`
- `/backend/src/modules/combat/`
- `/backend/src/modules/gacha/`
- `/backend/src/modules/quests/`
- `/backend/src/modules/pve/`

## Goal
The actual "game": hero system, combat resolution, gacha/summon economy, PvE
monster hunting, and quests/daily tasks.

## Deliverables
1. **Heroes** — hero catalog, leveling/XP curve, star/ascension system, gear
   slots, stat calculation.
2. **Combat** — deterministic battle resolution given two troop/hero
   compositions (attack/defense/HP formulas, troop-type advantage matrix,
   randomness seeded for reproducibility/anti-cheat). Emits a `battle:result`
   internal event for `05-realtime` to push.
3. **Gacha** — summon system with configurable drop-rate tables, pity
   counter, currency cost, and provably-fair random seed logging (important:
   log the seed/roll server-side for auditability).
4. **PvE** — monster/dungeon nodes on the map, difficulty scaling, rewards.
5. **Quests** — daily/weekly quest definitions and progress tracking.
6. Unit tests for combat math and gacha probability distribution (statistical
   test over N rolls approximating configured rates).

## Constraints
- Combat and gacha must be server-authoritative — never trust client-submitted
  outcomes, only inputs (attacker/defender IDs, summon request).
- Don't build the city/resource/training loop — that's `04-backend-core`.

## Definition of done
An attacker can hit a PvE node or another player's city and get a
deterministic, server-computed result; a gacha pull draws from the configured
rate table and the pity counter behaves correctly across repeated pulls in tests.
