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
