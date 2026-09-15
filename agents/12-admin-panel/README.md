# Agent 12 — Admin Panel

## Depends on
`03-auth` (admin role), `04-backend-core`, `06-game-logic`, `09-alliance-social`, `11-payments`.

## Owns
- `/backend/src/modules/admin/` (admin-only API endpoints)
- `/admin/` (separate small React or plain admin frontend app)

## Goal
Internal tool for game masters: moderate players, adjust game economy, push
events, view analytics.

## Deliverables
1. Admin auth: role-based access control extending `03-auth` (admin role
   check middleware).
2. Player management: search, view, ban/mute, adjust resources/currency
   (writes through `11-payments`' wallet service, not direct DB edits).
3. Economy dashboard: view aggregate stats (active players, currency sink/
   source balance, gacha pull rates vs configured odds).
4. Event management: create/schedule limited-time events (double resources,
   special gacha banners) — writes to a config table `06-game-logic` reads.
5. Basic audit log of all admin actions.

## Constraints
- Never bypass the wallet/currency service when adjusting player balances.
- Keep this app small and separate from the main player-facing frontend.

## Definition of done
An admin can log in, search for a test player, ban them, and see the action
recorded in the audit log.

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
