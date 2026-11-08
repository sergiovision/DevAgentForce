# Settings and environment

**Settings** (`/settings`): General, Backup & Restore, License, System LLM, Memory, Database, then one area per `.env` group. Secrets: `/secrets`.

## General

- **Global mode** — `autonomous`, or `interactive` (Pro: plan approval).
- **Pause / Resume queue** — running tasks finish, nothing starts. Before restarts or during outages.
- **Notify me about new versions** — on; footer notice with the install command (*Updating*). Off = no notice anywhere.
- **System LLM: Vendor | Model | Billing** — Fill Task, DevPlan, graph decompose/rollup, compaction, Ask Agent. Default Anthropic. *Max* = subscription login; *API Platform* = key.

## Environment editor

With an encryption key, saves sealed (e.g. `global/PGUSER`) and clears `.env`; without, edits `.env`. Restart the worker after changes.

| Key | For |
|---|---|
| `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `GEMINI_API_KEY` | API billing only |
| `GITEA_TOKEN`, `GITHUB_TOKEN` | Global; per-repo overrides |
| `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID` | Telegram |
| `DISCORD_WEBHOOK_URL` | Discord |
| `GIT_USER_EMAIL`, `GIT_USER_NAME` | Agent commit author |
| `PGHOST`, `PGPORT`, `PGUSER`, `PGPASSWORD`, `PGDATABASE` | Database |
| `ENABLE_LOGIN_PAGE`, `LOGIN_NAME`, `LOGIN_PASSWORD` | Sign-in (*Signing in*) |

## Notifications

Telegram, Discord (opt-in via env): start, success, failure, failover; Pro adds budget and preflight alerts.

Telegram commands: `/status`, `/approve KEY`, `/reject KEY`, `/cancel KEY`, `/retry KEY`, `/pause`, `/resume`, `/mode`, `/help`. Pro: `/reply KEY <message>`, `/inbox`, `/digest`, `/budget KEY`.

## Setup and backup

- `/setup` — checks the DB, migrates, writes `.env`. All pages redirect there until done.
- **Backup & Restore** (also `/backup`, `/restore`, `devagentforce-admin backup|restore`) — one encrypted `.zip`: database, `.env`, secrets file and key, licence, skills if *Include skills*. Passphrase in the form, never chat. Restore keeps local connection, ports, folders, key; safety backup first; applies next start. Scheduled backups (off) need `BACKUP_PASSPHRASE`.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#first-run)
