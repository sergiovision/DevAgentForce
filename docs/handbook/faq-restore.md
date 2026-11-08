# FAQ — backup, restore and moving machines

Your data is safe at every step.

**Back up.** Settings → **Backup & Restore** → create. Passphrase (8+ chars) protects it and carries the secrets key. Host: `scripts/devagentforce-backup.sh` (`.ps1`) or `devagentforce-admin backup create`. Scheduled backups need `BACKUP_PASSPHRASE` in `.env` or the store. `/backup` lists them.

**Restore.** Settings → Backup & Restore → upload or pick → restore. *Staged*: passphrase checked, safety backup to `backups/safety/`, applied at **next worker start** before the database opens. Result: `backups/last-restore.json` (`/restore` here). Host: `scripts/devagentforce-restore.sh` — worker stopped, or `--stage` and restart.

**"wrong passphrase … (or the payload is damaged)".** Different passphrase, or truncated file — re-download. Automatic pre-update backups need none.

**"restore onto PostgreSQL N or newer".** Dump from a newer major. Upgrade the server. No override.

**Backup from a newer build.** Update first; `--force` restores anyway. Older backups migrate forward.

**"no PostgreSQL client tools … were found".** Needs `pg_dump`/`pg_restore`/`psql` ≥ server major. Set `PG_BIN_DIR` in `.env`, or install the client.

**Database part failed — data gone?** No. One transaction; rollback keeps the old DB; safety backup exists. *"restored, but the schema migration failed"* — data is in; run migrations, read the log.

**New machine.** Install there → back up *with* the key on the old one → restore → stop the old install (one at a time). The new host keeps its `DATABASE_URL`, `PG*`, ports, paths, `VAULT_*`; keys, tokens, settings, sign-in come from the backup.

**Memory and code index empty.** Backup lacked *Include repositories memory*. Reindex.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#faq-restore)
