# Agent 13 — Notifications

## Depends on
`03-auth`, `05-realtime` (push bridge), `04-backend-core`/`06-game-logic` (event sources).

## Owns
- `/backend/src/modules/notifications/`
- `/backend/src/jobs/scheduled-events.ts` (cron jobs)

## Goal
Push notifications, email digests, and scheduled/recurring game events
(daily reset, event start/end).

## Deliverables
1. Notification service: create/store notifications (building complete,
   under attack, alliance invite, gacha pity reached), deliver via
   `05-realtime`'s socket bridge when the player is online, store for later
   read when offline.
2. Email digest (optional/stubbed if no mail provider set up): daily/weekly
   summary email, opt-in/out setting.
3. Cron jobs: daily reset (quest refresh, login streak), scheduled event
   start/end triggers that write to the event-config table `06-game-logic`
   reads.
4. Notification preferences per player (which types to receive, mute options).

## Constraints
- Don't implement the socket transport itself — call into `05-realtime`'s
  bridge module.
- Keep cron jobs idempotent — safe to run twice if the scheduler retries.

## Definition of done
A simulated "building complete" event produces a stored notification and,
if the player is connected, a live push via the socket bridge; the daily
reset cron job runs and resets quest progress for all test players.
