# Agent Status Board

Shared memory across all 13 agent sessions. This file lives only on the
`dont-merge` branch (checked out at `lords-mobile-worktrees/planning`) —
never merge it into `main` or any `agent/*` branch.

**Rule for every agent:** before ending a work session, update your row below
(from the `planning` worktree, not your own agent worktree), commit, and
push to `dont-merge`:

```bash
cd /home/sanjey/Pictures/Script/clean_pages/lords-mobile-worktrees/planning
git pull origin dont-merge
# edit docs/STATUS.md — update your row only
git add docs/STATUS.md
git commit -m "status: agent-XX update"
git push origin dont-merge
```

If your row conflicts with someone else's edit on pull, that's expected with
13 agents touching one file — just re-apply your row and push again.

## Status table

| Agent | Branch | Status | Last commit | Blocked on | Notes |
|---|---|---|---|---|---|
| 01-architect | agent/01-architect | not started | - | - | Must finish before others start |
| 02-database | agent/02-database | not started | - | 01-architect | |
| 03-auth | agent/03-auth | not started | - | 01-architect | |
| 04-backend-core | agent/04-backend-core | not started | - | 01-architect, 02-database, 03-auth | |
| 05-realtime | agent/05-realtime | not started | - | 01-architect, 03-auth, 04-backend-core | |
| 06-game-logic | agent/06-game-logic | not started | - | 01-architect, 02-database, 04-backend-core | |
| 07-frontend-ui | agent/07-frontend-ui | not started | - | 01-architect | |
| 08-frontend-integration | agent/08-frontend-integration | not started | - | 07-frontend-ui, 03/04/05/06 | |
| 09-alliance-social | agent/09-alliance-social | not started | - | 02, 03, 04, 05 | |
| 10-devops-qa | agent/10-devops-qa | not started | - | 01-architect | |
| 11-payments | agent/11-payments | not started | - | 02, 03, 06 | |
| 12-admin-panel | agent/12-admin-panel | not started | - | 03, 04, 06, 09, 11 | |
| 13-notifications | agent/13-notifications | not started | - | 03, 05, 04/06 | |

## Status values
`not started` → `in progress` → `blocked` → `ready for review` → `merged`

## Cross-agent change requests
See `docs/CHANGE-REQUESTS.md` in this same branch for contract-change asks
between agents (e.g. "I need a new DB column" from 06 to 02).
