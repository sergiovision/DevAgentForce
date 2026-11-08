# Troubleshooting

Symptom, cause, fix.

## Database down

Red banner, empty dashboard, API 503 with `db` diagnostic. On the worker machine:

```bash
./scripts/dbrestart.sh
```

Handles launchd/systemd or a `pg_ctl` data dir; clears a stale `postmaster.pid` (*"lock file postmaster.pid already exists"*, crash-loop). Up but unreachable? Check `PGHOST`/`PGPORT` in `.env`.

## Stuck in `queued`

- Paused? Settings or Telegram `/status`.
- Waiting? `WORKER_CONCURRENCY` cap; local repo queues same-vendor tasks; unfinished `depends_on`.
- **Web** down when created → never dispatched. **Worker** down → nothing consumed.

## Failed at a gate

On purpose; the detail page says which.
- **PR preflight** — secret, file > 1 MB, or HEAD not by the configured git identity. Nothing pushed.
- **Budget exceeded** — cost or wall-clock ceiling.
- **Reality abstain** — evidence below your threshold; no run spent.
- **Plan rejected / timed out** — not approved in the window.

Fix, then **Continue** (same session) or **Re-run**.

## Agent issues

- **429** — in-call backoff, `rate_limit_backoff` events. Constant? Fewer concurrent tasks per vendor, or a **backup vendor**.
- **CLI "not found"** — install on the worker, on `PATH`, or switch vendor. Max billing: log in on the host once.
- **Out of turns** — raise **Max turns** or **Continue**. Recurring = under-specified.
- **Going in circles** — **Compact**: brief of tried, dead, next; clean conversation.

## Restart

```bash
./scripts/restart.sh --dev     # or --prod
./scripts/start.sh             # start only
./scripts/stop.sh              # stop and sweep orphans
./scripts/migrate.sh           # apply database migrations
```

Logs: `/logs` live; `logs/worker.log`, `logs/web.log`.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#troubleshooting)
