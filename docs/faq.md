# DevAgentForce FAQ

Answers for buyers, evaluators and operators. Live version: https://capitaltools.app/devagentforce/docs#faq. In the dashboard, type `/faq` or `/setup` in **Ask Agent**.

[Product](#product) · [Agents and billing](#agents-and-billing) · [Git and repositories](#git-and-repositories) · [Security](#security) · [Setup and operations](#setup-and-operations) · [Troubleshooting](#troubleshooting)

## Product

**What does DevAgentForce do?**
You describe a task. An agent CLI works in its own worktree with only the secrets it needs.
Your build, tests and lint check it; failures retry with a hint; a PR opens. See [use cases](../use-cases/README.md).

**Free vs Pro?**
Free is a complete pipeline: queue, four vendors with failover, retries, dashboard, Skills, schedules, all git flows and hosts, MCP, vault, backup. Runs on API keys.
Pro adds subscription billing, Sessions, memory search, workflows, review loop, budget breaker, PR preflight, rich Telegram, A2A and more. Full split: [Editions](editions.md).

**Do I need a Pro licence?**
No. A new install runs Free with no sign-up. Pro features stay off.

**Is there a free trial?**
Yes. 14 days of Pro from your capitaltools.app account. When it ends, Pro switches off. Nothing is deleted.

**Where does it run?**
Natively on Linux, macOS or Windows, on PostgreSQL 16+ with pgvector. A small desktop is enough. Desktop app available. See [Getting started](getting-started.md).

**Which interface languages?**
Nine: English, Spanish, Brazilian Portuguese, Russian, German, Japanese, Korean, Simplified Chinese, Arabic (right-to-left).
Follows your browser unless pinned in Settings.

**Can it run scripts without an agent?**
Yes. Run a script task from **Scripts**: no queue, no LLM spend, live redacted output. Or queue it for an agent. See [Schedules and scripts](features/schedules-and-scripts.md).

**What are Skills?**
Reusable `SKILL.md` procedures in the open Agent Skills format. Run one as a task, attach it, or let the agent pick.
Presets: code review, TDD, bug diagnosis, design interview. **Save as skill** turns a task into one. See [Skills and artifacts](features/skills-and-artifacts.md).

**Is it still evolving? How do I report a bug?**
Yes, regular releases ([changelog](https://capitaltools.app/devagentforce/changelog)). Licensed users file bug reports with logs from the Logs page.

## Agents and billing

**Which agents are supported?**
Claude Code, OpenAI Codex, Google Antigravity (Gemini) and Pi. Chosen per task or template.
Pi covers any OpenAI-compatible endpoint: OpenRouter, Groq, DeepSeek, xAI, Mistral, Ollama, LM Studio, vLLM. See [Agent backends](features/agent-backends.md).

**Do I need an API key?**
On Free, yes. Pro adds subscription (Max) billing: the CLI uses your Claude Max, ChatGPT Plus or Google AI Pro/Ultra login.
That login must exist on the worker machine. Pi always bills by API key.

**Which vendor first?**
The CLI you already have logged in. Set a **backup vendor** for automatic failover on rate limits.

**What does it cost to run?**
Your licence (Pro) plus your AI vendor's charges. We never resell inference. Memory search is local and free.
Dashboard shows total, per-PR and per-task cost. On subscription billing cost reads zero; token charts still show size.

**Grok, DeepSeek or local models?**
Yes, through Pi: Settings → Vendors, add an endpoint, **Test**, pick Pi on the task. Local servers need no key.
Pi is OS-sandboxed on macOS and Linux. On Windows, run untrusted repos on a disposable VM.

**Several agents on one project at once?**
Yes. Different vendors share a repo in parallel, each in its own worktree.
Pro Sessions shows every Claude Code, Codex and Antigravity session on the host: live transcripts, tokens, plan approval, steering.

## Git and repositories

**Which git hosts?**
Gitea, GitHub (incl. Enterprise Server), Azure DevOps (cloud and Server), and Local Git. Host detected from the URL.
Tokens are never shared across providers. See [Git providers](features/git-providers.md).

**Without a git host?**
Yes. Local Git is any existing clone — GitLab, Bitbucket, NAS. All four flows work; nothing is pushed unless Branch + PR finds a usable origin.
See [use case 04](../use-cases/04-local-repo-no-remote.md).

**What if an agent breaks my repository?**
Remote repos: it works in an isolated worktree, and nothing lands without your PR review. Local Git: never reset, cleaned or pushed on its own.
Direct commit and Patch refuse a dirty tree; direct commit refuses a detached HEAD. Pro PR preflight blocks secrets, large files and out-of-scope changes.

**Can a task span several repositories?**
Yes, limited by design. `@repo_name` gives read-only access. Write access comes from dependent folders set by the repo owner, not the task. See [Cross-repo work](features/cross-repo.md).

## Security

**How are secrets kept from LLMs?**
Five layers: encrypted vault (never returned by the API), redaction in prompts, logs and messages, per-task secret grants (Pro), Pro PR preflight scan, masked host paths.
See [Secrets vault](features/secrets-vault.md).

**Does my code leave my network?**
Only to the AI vendor you chose, under your account. Capital Tools never sees your code, repos or prompts. Embeddings run locally.

**Without internet?**
Yes, apart from your AI vendor — or a local model via Pi. Air-gapped hosts can activate Pro offline.

**Can agents use my other tools — docs, tickets, data?**
Yes, every edition. Add an external MCP server per repo. Read-only tools are allowed; data-changing tools stay off until enabled; every call is audited.
A server whose tools change is paused and the difference shown. See [MCP](features/mcp.md).

**A sign-in screen for the dashboard?**
Set `ENABLE_LOGIN_PAGE` with a login and password. Both services bind `LISTEN_HOST` (localhost by default).
Expose via reverse proxy or private network. See [handbook: access](handbook/access.md).

## Setup and operations

**What does it need?**
PostgreSQL — the native installer can install a private one. At least one agent CLI on the worker machine.

**Something is not configured. Where do I start?**
Type `/setup` in Ask Agent. It checks database, migrations, secrets, AI providers, git tokens, notifications and paths, and lists what is missing.

**Which database settings are used?**
`DATABASE_URL`, else the `PG*` variables. Lookup order: process environment, `.env`, secrets store.
A value exported in the shell beats an edited `.env`. Restart to apply.

**Do I run migrations?**
Usually not. The worker migrates at start. Manual runs also work.

**How do I set up and protect the secrets store?**
The vault key is created on first boot. Move values in with **Import from .env** on Secrets, then restart.
Save the recovery key (`/setup` → *Show recovery key*). Lose it, lose the secrets. See [handbook: secrets FAQ](handbook/faq-secrets.md).

**Back up, restore or move machines?**
Settings → **Backup & Restore** makes an encrypted archive; a passphrase lets it carry the vault key. Restore is staged, takes a safety backup, applies at next worker start, in one transaction.
New machine: install, then restore. It keeps its own connection settings, ports and key. See [Backup and restore](features/backup-restore.md).

**How do I update?**
Re-run the installer, or Settings → Updates. Data stays. A bad build rolls back. Updating twice is safe.
See [handbook: updating](handbook/updating.md) and https://capitaltools.app/devagentforce/docs#updating.

## Troubleshooting

**I created a task and nothing happened.**
The dashboard enqueues; the worker consumes. Dashboard was down: **Re-run**. Worker down: task stays `queued`.
Check the queue is not paused (Settings or Telegram `/status`) and no concurrency limit or dependency holds it.

**A task is stuck in `running`.**
Open its page; the session tail shows if the agent is working. Dead workers are detected and tasks reclaimed.
To act now: **Cancel**, then **Re-run** or **Continue**.

**Re-run, Continue or Compact?**
**Re-run** starts fresh. **Continue** resumes the same session. **Compact** restarts from a short summary — for runs going in circles.

**My task failed without the agent doing much.**
A gate stopped it; the task page names it: preflight, budget ceiling, rejected plan, or abstain on an under-specified task. Fix it, then **Continue**.

**After a worker restart my tasks are `pending`.**
By design. Nothing stays half-owned. **Re-run** the ones you want.

**An agent CLI is "not found".**
Install it on the worker machine and add it to that machine's `PATH`. For subscription billing, log in there once.

**The database is down or shows a red banner.**
Restart PostgreSQL; the bundled scripts clear a stale lock file. Ask Agent still answers meanwhile.

**"N secrets cannot be decrypted".**
The loaded vault key is not the one that sealed them. Supply the old key with the current one, restart, re-seal. See [handbook: secrets FAQ](handbook/faq-secrets.md).

More: [troubleshooting](handbook/troubleshooting.md) · [queue FAQ](handbook/faq-queue.md) · [setup FAQ](handbook/faq-setup.md) · [restore FAQ](handbook/faq-restore.md) · https://capitaltools.app/devagentforce/docs#troubleshooting

## Related

[Getting started](getting-started.md) · [Editions](editions.md) · [Feature catalogue](features/README.md) · [Handbook](handbook/README.md) · capitaltools.app: [FAQ](https://capitaltools.app/devagentforce/docs#faq) · [Docs](https://capitaltools.app/devagentforce/docs) · [Product](https://capitaltools.app/devagentforce)
