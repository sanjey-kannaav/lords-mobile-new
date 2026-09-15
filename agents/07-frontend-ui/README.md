# Agent 07 — Frontend UI

## Depends on
`docs/spec.md`, `docs/api-contract.md` (types/shapes only — can mock responses).

## Owns
- `/frontend/src/components/`
- `/frontend/src/pages/`
- `/frontend/src/styles/`
- `/frontend/src/assets/`

## Goal
Build the React UI for every screen using mocked/stubbed data, so this can
run fully in parallel with backend work. `08-frontend-integration` will later
swap mocks for real API calls.

## Deliverables
1. **City/base view** — building grid, upgrade buttons, resource bars, timers (visual countdown, ok to be fake data).
2. **Hero screen** — roster, hero detail, leveling/upgrade UI, gacha/summon animation screen.
3. **Troop/training screen** — queue list, training UI.
4. **Map/world view** — pannable/zoomable map, other players' cities, monster nodes.
5. **Alliance screen** — member list, chat panel, alliance war board.
6. **Shop/store** — currency purchase UI (no real payment wiring yet).
7. **Auth screens** — login/register/forgot-password forms.
8. Global layout: nav bar, notifications tray, modals, toasts.
9. State management setup (Zustand/Redux) with a clean "data layer" boundary
   (hooks like `usePlayer()`, `useCity()`) that currently return mock data but
   are structured so `08-frontend-integration` only needs to swap the
   implementation inside those hooks, not every component.

## Constraints
- Do not write actual `fetch`/`axios` calls to backend endpoints — use the
  mock-data hook pattern described above so integration is a clean swap.
- Follow `docs/api-contract.md` field names exactly in your mock data/types
  so integration doesn't require renames.

## Definition of done
Every screen in `docs/spec.md`'s v1 feature list is clickable end-to-end with
mock data, responsive, and uses the `use<Thing>()` hook boundary pattern.
