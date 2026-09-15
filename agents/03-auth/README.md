# Agent 03 — Auth

## Depends on
`docs/api-contract.md` (auth endpoints), `02-database`'s `users` table.

## Owns
- `/backend/src/modules/auth/`
- `/backend/src/middleware/auth.ts`

## Goal
User registration, login, session/JWT auth, password reset, and route
protection middleware used by every other backend module.

## Deliverables
1. `POST /api/v1/auth/register`, `/login`, `/logout`, `/refresh`, `/forgot-password`, `/reset-password`.
2. JWT access + refresh token flow (short-lived access token, rotating refresh token).
3. Password hashing (bcrypt/argon2), input validation, rate limiting on auth endpoints.
4. `requireAuth` Express/Nest middleware other agents import to protect routes.
5. Optional OAuth (Google) stub if time allows — behind a feature flag.
6. Unit tests for all auth flows.

## Constraints
- Only touch `/backend/src/modules/auth/` and the shared auth middleware —
  do not modify other modules' routes.
- Follow the exact request/response shapes in `docs/api-contract.md`; if they
  need to change, log it in `docs/CHANGE-REQUESTS.md`.

## Definition of done
All auth endpoints pass their tests; `requireAuth` middleware is documented
with a usage example other agents can copy.
