# FAQ — secrets setup and recovery

Keys, lost keys, values that will not change.

**Setup?** None. First boot creates the key in `VAULT_KEY_FILE`, else the shared folder. Missing? `/install-keys` here or **Install Keys** on Secrets. Then **Import from .env** (native: `devagentforce secure`), restart.

**"Encryption key is missing".** Secrets exist, key gone; new keys refused. Paste the recovery key into **Restore** (Secrets or Setup) — a wrong key changes nothing. Page cannot? `devagentforce-admin vault restore-key --stdin`, restart. Gone for good? Delete all from that screen, or `devagentforce-admin vault wipe --confirm="DELETE ALL SECRETS"`.

**"Install Keys": key already installed.** On purpose — a second key orphans the first's secrets. Rotate instead. A **blank** exported `VAULT_ENCRYPTION_KEY` outranks the key file — remove it.

**Save the recovery key.** `/setup` → *Show recovery key*. No back door. Passphrase-protected backups carry it too.

**"N secrets cannot be decrypted".** Wrong key loaded — new key generated, or `.env`/`VAULT_KEY_FILE` points elsewhere. Old key → `VAULT_ENCRYPTION_KEY_OLD` (comma-separated), current stays in `VAULT_ENCRYPTION_KEY`, restart, `devagentforce-admin vault rewrap`.

**Lost the vault key.** Restore from a backup with the key, or your recovery key. Neither: values gone — new key, re-enter secrets.

**"secrets are stored but no key is configured".** Check `VAULT_KEY_FILE`, default `~/.devagentforce/vault.key` (or `DEVAGENTFORCE_HOST_DEVAGENTFORCE` folder), and read access. Read-only fallbacks: working dir, `.env` folders, their `config/` subfolders.

**Changed a secret, nothing changed.** Process env → `.env` → store: delete the winning copy. Restart for boot-time settings.

**`DATABASE_URL` in the store?** Yes — encrypted file tier (`VAULT_FILE`, default `~/.devagentforce/vault.json.enc`), read before connecting. Survives Postgres down; not a lost key.

**Restoring onto another machine.** Host with a key keeps it and re-seals; host without adopts the backup's. Local `DATABASE_URL`, `PG*`, ports, `VAULT_*` always win.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#faq-secrets)
