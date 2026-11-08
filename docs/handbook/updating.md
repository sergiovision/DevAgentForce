# Updating the platform

Re-run the installer. That is the update.

```bash
curl -fsSL https://capitaltools.app/install.sh | bash        # macOS / Linux
irm https://capitaltools.app/install.ps1 | iex               # Windows PowerShell
```

Run on the host. Stops the service, replaces program files, applies the schema, restarts. Settings, `.env`, logs, worktrees and database stay. Desktop app: same. Dashboard and worker move together; a crossed pair gets a red *skew* marker in the footer.

**Upgrade note.** Agents no longer inherit custom secrets from the launcher — `vault export-env` prints only known settings and vendor keys; assign others. This release drops the `kind` column: no rollback, older workers cannot read database-tier secrets.

## New-build notice

**Settings → General → Notify me about new versions** (on). The worker checks capitaltools.app every few hours. On a new build:
- Dashboard: *"DevAgentForce build N is available — run this to update:"* above the footer, host-OS command (copy), other OS below.
- Desktop: one tray notification per build.
- Telegram / Discord: one message per release.

Dismiss = hidden for **that build**. Setting off = no notice anywhere.

It never updates itself: the worker runs AI-written code, so it never replaces or restarts itself.

**Confirm**: reload — notice gone, new build in the footer; worker log says `version changed since last boot`.

## No notice?

- Setting off, or dismissed.
- Source/dev run — no build number.
- No release for this OS/CPU.
- Source unreachable — last answer stands; retries itself.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#updating)
