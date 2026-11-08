# Desktop app

The native release in a window. macOS Apple Silicon, Windows x64, Linux x64. Shares `~/.devagentforce` — secrets, private PostgreSQL, tasks, licence — with the native install.

## Behaviour

- Native service running → attaches; Quit leaves it. Otherwise starts database, worker, dashboard itself.
- Closing the window keeps tasks running (tray).
- Windows: repairs a broken logon task once; still broken → runs services itself.
- macOS: agents get a private home without Desktop/Downloads — no privacy prompts (admin runs keep the real home). Downloads open the Save panel.
- The window never asks for sign-in, even with `ENABLE_LOGIN_PAGE=true`. Browsers still do, and return to it on expiry.
- No self-update. With *Notify me about new versions* on, the tray shows the install command; re-run it (*Updating*). Same fix for "database was updated by a newer DevAgentForce".

## Dictation

On-device. Model (base, ~140 MB) downloads once. No cloud key, no quota.
- **Cloud error (e.g. 402)** after attaching to a console service → tray → *On-device dictation for the console…*, restart the service.
- **Wrong language** (e.g. English written in Russian) → tray → *Dictation language* (or Settings → Dictation), not Auto-detect.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#install)
