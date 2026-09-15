# Agent 02 — Database

## Depends on
`docs/db-schema.md` from Agent 01.

## Owns
- `/backend/prisma/schema.prisma` (or equivalent ORM schema)
- `/backend/src/db/` (migrations, seeders, db client setup)

## Goal
Implement the PostgreSQL schema exactly as specified in `docs/db-schema.md`,
plus migrations and seed data so other backend agents have a working DB to
develop against immediately.

## Deliverables
1. ORM schema/models for every entity in `docs/db-schema.md`.
2. Migration scripts (versioned, runnable via `npm run migrate`).
3. Seed script with sample data: a few test players, base building types,
   base troop types, a small hero roster, sample items — enough for
   `04-backend-core` and `06-game-logic` to build and test against.
4. Indexes for hot paths (leaderboards, player lookups, alliance membership).
5. A `docs/db-schema.md` amendment note (via `docs/CHANGE-REQUESTS.md`) if the
   real schema needed to diverge from the architect's draft.

## Constraints
- Do not touch `/backend/src/routes` or business logic — schema/migrations only.
- Keep migrations additive/reversible; never hand-edit a migration that's
  already been applied by another agent — add a new one.

## Definition of done
`npm run migrate && npm run seed` succeeds from a clean database and produces
data matching the seed spec above.
