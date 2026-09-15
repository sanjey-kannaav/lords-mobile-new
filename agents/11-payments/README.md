# Agent 11 — Payments

## Depends on
`03-auth`, `02-database`, `06-game-logic` (gacha currency costs).

## Owns
- `/backend/src/modules/payments/`
- `/backend/src/modules/wallet/`

## Goal
Virtual currency (gems/gold), in-app purchase flow, and transaction ledger.

## Deliverables
1. Wallet system: per-player currency balances (soft currency = gold earned
   in-game, hard currency = gems bought with real money), atomic
   credit/debit operations (DB transaction-safe, no race conditions on
   concurrent spends).
2. Store catalog: currency packs, special offers, starter pack.
3. Payment provider integration (Stripe for web, or a mock/sandbox provider
   if no real merchant account exists yet) — webhook handling for payment
   confirmation, idempotent order processing.
4. Transaction ledger table: every currency change logged with reason
   (purchase, gacha pull, quest reward, admin adjustment) for auditability.
5. Refund/chargeback handling stub.

## Constraints
- All balance changes must go through the wallet module's atomic
  credit/debit functions — no other module should write to balance columns
  directly. Expose a small internal API (`walletService.debit(...)`) for
  `06-game-logic`'s gacha module to call.
- Never trust client-submitted currency amounts — server computes cost from
  the store catalog.

## Definition of done
A test purchase flow (sandbox payment) credits the correct currency amount
exactly once even under retried webhook delivery; a gacha pull correctly
debits currency via the wallet service.

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
