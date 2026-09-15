# Agent 10 — DevOps & QA

## Depends on
`01-architect`'s repo scaffolding decisions. Runs continuously alongside all other agents.

## Owns
- `/docker-compose.yml`, `/backend/Dockerfile`, `/frontend/Dockerfile`
- `/.github/workflows/` (CI)
- `/backend/test/` test infra config (Jest/Vitest setup, not individual test cases — those belong to each module's owning agent)
- `/scripts/` deploy & utility scripts

## Goal
Make the project runnable locally with one command, tested automatically on
every change, and deployable.

## Deliverables
1. `docker-compose.yml`: Postgres, Redis, backend, frontend, with hot-reload
   for local dev (`docker compose up` just works).
2. CI pipeline (GitHub Actions): lint, typecheck, unit tests, build, on every
   PR; block merge on failure.
3. Test infra: Jest/Vitest config, coverage thresholds, a shared test-db
   setup/teardown helper other agents' tests can import.
4. Load testing script (k6 or Artillery) for the core loop (login, fetch
   city, queue build) with a documented baseline.
5. Deployment scripts/docs for at least one target (e.g. Docker image push +
   a simple VPS/PaaS deploy, or notes for Railway/Render/Fly.io).
6. `docs/RUNBOOK.md` — how to run locally, run tests, deploy, and roll back.

## Constraints
- Don't write feature test cases yourself — provide the test *infrastructure*
  each module agent hooks their own tests into.
- Keep CI fast; parallelize test jobs per backend/frontend.

## Definition of done
A fresh clone + `docker compose up` gives a working local stack; CI runs and
passes on a clean PR; `docs/RUNBOOK.md` exists and is accurate.

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
