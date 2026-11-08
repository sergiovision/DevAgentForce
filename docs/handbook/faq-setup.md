# FAQ — setup, configuration and database

Configuration, database and port fixes.

**Where to start?** `/setup` here scans database, migrations, secrets, AI providers, git tokens, notifications, worker paths. Forms: `/setup` page (`/setup?force=1` reopens).

**Which database settings?** `DATABASE_URL` wins. Else `PGHOST` (127.0.0.1), `PGPORT` (5432), `PGUSER`, `PGDATABASE` (`devagentforce`) — only with `PGPASSWORD` set. Lookup: process env → `.env` → secrets store; a shell export beats `.env`. Restart after changes.

**"password authentication failed for user devagentforce".** Role missing or password mismatch. Correct the password in `.env`/secrets store, or `ALTER ROLE devagentforce PASSWORD '…'`, restart. Windows: `scripts/setup-local.ps1` recreates the role.

**pgvector errors / "extension vector is not available".** Needs PostgreSQL 16+ with pgvector. `devagentforce-admin db check` exits: **3** not installed · **4** PostgreSQL too old · **6** login cannot enable it — run `CREATE EXTENSION vector;` once as superuser in the platform database.

**"lock file postmaster.pid already exists" / crash-loop.** `scripts/dbrestart.sh` restarts (service or data dir) and clears the stale file. Bundled DB: `devagentforce db status`, `db start`, `logs db`.

**Migrations?** Automatic at worker start (`MIGRATE_ON_START`, default on). By hand: `scripts/migrate.sh` or `devagentforce migrate`. Refused while a session is *idle in transaction* on `tasks` — close it (stuck psql, IDE), retry.

**Red database banner, API 503.** Postgres down — see above. Ask Agent still works; it skips the database.

**"VERSION SKEW".** Dashboard and worker builds differ. Update both (*Updating*), restart.

**Port 3200/8000 taken.** Dashboard `WEB_PORT`, worker `WORKER_PORT`. `scripts/stop.sh` frees them if this install holds them; else change the port in `.env`, restart.

**Agent CLI "not found".** Install on the worker host, on `PATH`. Max billing: log in there once (`claude login`, `codex login`).

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#faq-setup)
