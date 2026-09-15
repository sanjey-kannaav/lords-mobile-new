# Agent 08 — Frontend Integration

## Depends on
`07-frontend-ui`'s `use<Thing>()` hook boundary, real backend APIs from
`03-auth`, `04-backend-core`, `05-realtime`, `06-game-logic`.

## Owns
- `/frontend/src/api/` (API client, axios/fetch wrappers, React Query setup)
- `/frontend/src/hooks/` (implementations of the data hooks defined by `07-frontend-ui`)
- `/frontend/src/sockets/` (Socket.io client wiring)

## Goal
Replace mock data in the frontend with real backend calls and live
WebSocket updates, without needing to touch component code in
`07-frontend-ui`'s owned folders.

## Deliverables
1. Typed API client generated/derived from `docs/api-contract.md`.
2. React Query (or equivalent) setup: caching, retries, optimistic updates
   for actions like "collect resources" or "start training".
3. Auth flow wiring: login/register calling real endpoints, token storage
   (httpOnly cookie preferred; document choice), auto-refresh, protected routes.
4. Socket.io client: connect on login, subscribe to chat/notification/battle
   events, update UI state/cache on incoming events.
5. Error/loading/empty states wired through the existing UI components.
6. E2E smoke test (Playwright/Cypress): register → login → view city →
   queue an upgrade → see it complete.

## Constraints
- Do not redesign UI components — only implement the hooks/data layer they
  already expect.
- If a hook's expected data shape doesn't match the real API, fix it in the
  hook implementation, not by changing the API contract (file a change
  request instead if the contract itself is wrong).

## Definition of done
The app works against the real backend end-to-end with no mock data
remaining; the E2E smoke test passes.
