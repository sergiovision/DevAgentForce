# Getting started

Zero to first verified change. About fifteen minutes. Full guide: [capitaltools.app/devagentforce/docs](https://capitaltools.app/devagentforce/docs#install).

## 1. Check

- [ ] Linux x64, macOS (Apple silicon) or Windows (x64 / ARM64) — or one cloud VM.
- [ ] One agent CLI signed in or keyed: `claude`, `codex`, `agy` or `pi`.
- [ ] Git host token — only for pull requests. Local folders need none.
- [ ] PostgreSQL — optional. The installer brings its own.

## 2. Install

**Native** — recommended.

```bash
curl -fsSL https://capitaltools.app/install.sh | bash        # macOS / Linux
irm https://capitaltools.app/install.ps1 | iex               # Windows PowerShell
```

Options after `bash -s --`: `--key <licence>` · `--database-url <url>` · `--port <port>` · `--local-only` · `--no-service`

**Desktop app** — same release, native window, tray, on-device dictation. [Download](https://capitaltools.app/account/downloads) · [More](features/desktop-app.md)

**Cloud VM**

```bash
curl -fsSL https://capitaltools.app/install.sh | bash -s -- --local-only
sudo loginctl enable-linger "$USER"     # keep running after logout
```

Reach it over a private network (Tailscale) or a TLS proxy. Keep sign-in on. Never expose worker or database ports.

## 3. First run

1. Open `http://localhost:3200`. Setup opens first.
2. Fill each Setup item. Secrets go in the form, not a chat.
3. Save the vault recovery key.
4. Stuck? Ask Agent → `/setup`.

`.env` keys, if you prefer a file (placeholders):

```dotenv
ANTHROPIC_API_KEY=<your-key>
GITHUB_TOKEN=<token>            # pull requests on GitHub only
ENABLE_LOGIN_PAGE=true          # sign-in screen
TELEGRAM_BOT_TOKEN=<bot-token>  # optional alerts
```

Then `devagentforce secure` moves them into the vault.

## 4. First task

1. **Repos → + Add Repository → Local Git.** Pick a clone. Choose *Patch*. No token. No remote.
2. Dashboard shows the worker **online**.
3. **+ New Task.** One behaviour. One acceptance criterion.
4. Watch the timeline. Message the agent. Stop it anytime.

> First time? Run a `research` or `skill` task. No repo, no PR — proves your CLI works.

## 5. First pull request

1. Add a Gitea, GitHub or Azure DevOps repo: clone URL + token.
2. Set build, test and lint commands. That's "verified".
3. Choose **Branch + PR**. Run. Checks pass → PR opens.

[Git providers](features/git-providers.md) · [Ticket to verified PR](../use-cases/01-ticket-to-verified-pr.md)

## Updating

Re-run the installer. Settings, data and secrets stay. A dashboard notice shows the command when a build is out.

## Next

[Handbook: setup](handbook/getting-started.md) · [Native install](handbook/native.md) · [Troubleshooting](handbook/troubleshooting.md) · [Editions](editions.md) · [FAQ](faq.md)
