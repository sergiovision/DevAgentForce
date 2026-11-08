# Native install

One command, any machine. No Docker image — servers and VMs use it too.

```bash
curl -fsSL https://capitaltools.app/install.sh | bash        # macOS / Linux
irm https://capitaltools.app/install.ps1 | iex               # Windows PowerShell
```

Downloads this OS/CPU's release, checks sha256, registers a per-user service. Node bundled. No `--database-url` → private PostgreSQL + pgvector.

Options after `bash -s --` (Windows: `& ([scriptblock]::Create((irm https://capitaltools.app/install.ps1))) -Key …`): `--key <licence>` (Pro), `--database-url`, `--port`, `--local-only`, `--no-service`.

## Where things live

- Program: `~/.local/share/devagentforce/runtime` (systemd `--user` or LaunchAgent) · Windows `%LOCALAPPDATA%\DevAgentForce\runtime` (logon Scheduled Task).
- `.env`, data, logs: `~/.devagentforce` · Windows `%USERPROFILE%\.devagentforce`. Logs: `logs/{worker,web}.log`.
- Shared: `vault.key` (back it up), `vault.json.enc` (`DATABASE_URL`, sign-in, `INTERNAL_API_TOKEN`; `.env` keeps paths/ports), private DB (`pgsql/`, `pgdata/`, `postgres.env`).
- Desktop app: same layout. Older installs move on next install, or `devagentforce migrate-layout`.

## Private PostgreSQL

`--bundled-db` (`-BundledDb`) — own service on `127.0.0.1:5433` (next free port). Used unless you pass `--database-url` (pgvector checked) or `--admin-database-url` / `--use-local-postgres` (creates user, database, pgvector; also /setup → *Use my own PostgreSQL*). Updates never touch it. **No uninstall deletes it.** Launcher: `db start|stop|status`.

## Operate

- `~/.devagentforce/scripts/start.sh` (`restart.sh`, `stop.sh`) · Windows `scripts\start.ps1` etc. in `%LOCALAPPDATA%\DevAgentForce`. Print the addresses; ignore `--dev`/`--prod`.
- Dashboard binds `127.0.0.1:3200`; worker loopback only. `--listen-all` (`-ListenAll`) binds `0.0.0.0`; Windows firewall admits 3200 from Tailscale only.
- Sign-in is on — choose it via the one-time link (`devagentforce setup-link` for a new one).
- Secrets in `.env`? `devagentforce secure` (or /setup → *Move secrets to the vault*).
- Update: re-run the installer (*Updating*). Uninstall: `scripts/uninstall.sh` (`.ps1`); `--keep-data` (`-KeepData`), `--purge-secrets` (`-PurgeSecrets`) also deletes the shared vault.

## Problems

- **"has no archive for …"** — no build for this OS/CPU. Windows on ARM falls back to x64.
- **Tailscale peer cannot connect** — dismissed firewall prompt left a block rule. Re-run the installer.
- **macOS: app is damaged** — `xattr -d com.apple.quarantine <folder>`.

Full guide: https://capitaltools.app/devagentforce/docs

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#native)
