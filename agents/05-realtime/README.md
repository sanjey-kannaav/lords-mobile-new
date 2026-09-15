# Agent 05 — Realtime

## Depends on
`docs/websocket-events.md`, `03-auth` (socket auth), `04-backend-core` running.

## Owns
- `/backend/src/realtime/` (Socket.io gateway/server setup)
- `/backend/src/modules/chat/`
- `/backend/src/modules/notifications/socket-bridge.ts`

## Goal
WebSocket layer for chat, live notifications, troop-movement updates, and
battle-result pushes.

## Deliverables
1. Socket.io server with JWT-based handshake auth (reuse `03-auth` tokens).
2. Global chat, alliance chat, and private message channels with persistence
   (chat_messages table — coordinate with `02-database` via a change request
   if the table doesn't exist yet).
3. Server→client events per `docs/websocket-events.md`: `troop:moving`,
   `troop:arrived`, `battle:result`, `notification:new`, `chat:message`.
4. Presence tracking (online/offline per player) for alliance member lists.
5. Reconnection/backoff handling documented for the frontend team.

## Constraints
- Don't implement combat resolution logic itself — just relay events emitted
  by `06-game-logic`/`04-backend-core` via an internal event bus (e.g. Node
  EventEmitter or Redis pub/sub) so those modules don't need to import Socket.io directly.

## Definition of done
Two authenticated clients can exchange a chat message in real time, and a
simulated "battle finished" internal event results in both participants
receiving a `battle:result` push.
