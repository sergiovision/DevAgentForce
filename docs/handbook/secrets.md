# Secrets — the encrypted store

Every credential sealed in one place, AES-256-GCM. Values **never return over HTTP** — lists show fingerprint, key version, metadata. Page: **Secrets** (`/secrets`).

## The key

Created on first boot in the shared folder. If not:
- **Ask Agent** (Pro): "generate the secrets store encryption key" — approve; applied, no restart. You see only the fingerprint.
- **Install Keys** on Secrets.

Both refuse if a key exists — a second key orphans the first's secrets. **Lose the key, lose the secrets.** Save the recovery key; Backup & Restore files carry it too.

## Lookup and scopes

`process environment` → `.env` → `secrets store`. Migrate one at a time: store, then delete from `.env`. A stale shell export is the usual reason a rotated value changes nothing.

Address `<scope>/<NAME>` (*Full Secret Reference*): `global/ANTHROPIC_API_KEY` (replaces `.env`), `env:prod/DATABASE_URL`, `repo:7/GITEA_TOKEN`, `worker:3/A2A_TOKEN` (Crew member), `peer:acme/HMAC`.
- Resolution `env:<active>` → `repo:<id>` → `global`. **Exact match only.** `DEVAGENTFORCE_ENVIRONMENT` names the active one.
- Launchers export only known settings and vendor keys. Other secrets must be assigned to reach an agent.

## Editor

Tabs *All*, *Global*, *Env*, *Repo*, search, Environment filter. `worker:`/`peer:` live under *All*.
- **Add Secret** — scope, qualifier, name, value.
- **Edit** — version, fingerprint, last rotated. Empty keeps; new value rotates. Eye icon reveals — only place in the UI.
- **Import from .env** — *Safe Import* copies; *Import and Clear* also blanks `.env`.
- **Render .env** (Pro) — plaintext `.env` for one environment, mode 0600, for stacks that cannot read the store.

## Backends and rotation

`VAULT_BACKEND`: `db` (`vault_secrets`), `file` (`VAULT_FILE`), `both` (default). The file tier holds `DATABASE_URL` when it is a stored secret.

Rotate (per-secret `key_version`, no re-entry): old key → `VAULT_ENCRYPTION_KEY_OLD`, new → `VAULT_ENCRYPTION_KEY`, run `devagentforce-admin vault rewrap`. *"N secrets cannot be decrypted"* = old key missing.

## Redaction and access

- Known values (8+ chars) stripped by exact match from agent output, logs, messages. Preflight blocks a push carrying one.
- A task gets its repo's allowed refs ∩ what it asks for (Pro), in the CLI subprocess env only.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#security)
