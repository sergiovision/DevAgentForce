# FAQ — stuck tasks and the queue

Tasks that will not start, will not finish, or reset.

**Stuck in `queued`.** Check in order:
1. Queue **paused**? Settings or Telegram `/status`. An update keeps it paused.
2. **Worker** up? `/logs`.
3. Waiting? Max `WORKER_CONCURRENCY` (default 2); **local** repo runs same-vendor tasks one by one; unfinished `depends_on` defers.
4. Else wait 5 min — a `queued` task with no job returns to `pending` and re-enqueues.

**Stuck in `running`.** The session tail shows if the agent still works. Dead workers are caught:
- Job reclaimed after 3 min without heartbeat.
- Idle past repo timeout (default 60 min) → `pending` (checked every 15 min).
- Longer → `failed`, *"no worker activity"*.

Now: **Cancel**, then **Re-run** or **Continue**.

**Tasks went `pending` after a worker restart.** Start/restart/stop from the dashboard resets `running`, `verifying`, `queued` to `pending`, cancels jobs, drops repo locks. Not re-queued — **Re-run** or Continue.

**Created while the dashboard was down.** Only web enqueues. **Re-run**.

**Re-run / Continue / Compact.** Fresh attempt / same session, keeps learning / history → brief, clean conversation (for circles).

**`pending`, waiting for me.** A plan or side-effect decision — button on the detail page. Or reset by restart — **Re-run**. No `blocked` state.

**"address already in use".** Old worker holds 8000. `scripts/stop.sh` frees 3200/8000 (this install only), then `scripts/start.sh`.

**Everything stuck.** `scripts/restart.sh` (native) or `--dev`/`--prod` in a checkout, then **Re-run**. Database? See *FAQ — setup, configuration and database*.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#faq-queue)
