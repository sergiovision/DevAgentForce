# Setup and first run

Unsure what is left? **Ask Agent** → *Set up* (or `/setup`) lists it in fix order.

## Needs

- **PostgreSQL 16+** with `pgvector`.
- **Node.js 22 LTS**, **Go 1.27+** — source builds only.
- **An agent CLI** — `claude`, `codex`, `agy` or `pi` — with API key or login.
- **Git host token** — only for PRs. **Local Git** needs none.

## Install

- **Native** (least work, optional private PostgreSQL): `curl -fsSL https://capitaltools.app/install.sh | bash` · Windows `irm https://capitaltools.app/install.ps1 | iex`. See *Native install*.
- **Desktop app** — same release, native window. See *Desktop app*.
- **Cloud VM** — native with `--local-only`, then Tailscale or a TLS proxy (Nginx, Caddy) to `127.0.0.1:3200`. Open 80/443; 22 to your address only.
- **Source** — for local changes:

```bash
cp config/.env.example .env       # at minimum set PGPASSWORD
./scripts/migrate.sh              # create/upgrade the schema
./scripts/start.sh --dev          # or --prod
```

## First run

1. Open `http://localhost:3200` — redirects to `/setup` until done.
2. Work the checklist. Secrets go in its forms, never chat. *Finish setup* needs every Needed item and the saved recovery key. `?wizard=1` = old wizard.
3. `/repos` → **Local Git** on an existing clone, *Patch only*. Gitea/GitHub need URL + token.
4. Toolbar shows worker online/offline and queue depth. Offline = nothing leaves `queued`.
5. **+ New Task** — one file, one behaviour, clear criterion, a vendor you have credentials for.
6. Watch the timeline, live log, runs.

Best first task: `research` or `skill` — no repo, no PR; proves CLI and credentials.

**Healthy**: worker **online**; `pending → queued → running` in seconds; `/logs` tails both. Stuck `queued`? One process is down — web writes the queue, worker consumes it.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#first-run)
