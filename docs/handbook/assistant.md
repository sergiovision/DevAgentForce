# About the Ask Agent assistant

The help panel, from the corner button on every page. **Free**, no licence.

## Runs anywhere

- **System LLM** (Settings → General) if usable; else the Claude Code CLI login or a `.env` API key. Works before the database or secrets store exists.
- Knows your page. On a task or repo page, answers about *that* one.
- Claude Code CLI: read-only tools — code/doc search, memory, decisions, transcripts, repo map, live task state. Other vendors: this handbook only, and it says so.

## Never acts alone

Every write is a card: **Run / Edit / Reject**. Nothing happens until Run; then it reports the real result, your edits included.
- Writes: task create/run/continue/retry/cancel, memory, ideas, templates, skills.
- Maintenance as named actions, never free-form shell: build, migrate, backup, database restart, restart, deploy. Restart and deploy run detached; output → deploy log.

## Commands

Enter sends; Shift+Enter new line. `/` commands and skills; `@` a task, repo, backlog folder or skill. Toolbar: History, Export → Markdown.
- **`/setup`** — scans database, migrations, secrets, AI providers and System LLM, git tokens and commit identity, Telegram, Discord, worker paths. Blockers first, one step at a time.
- **`/help`, `/mcp`, `/usage`, `/config`** (`/settings`) — panel and System LLM CLI.
- Add an MCP server for task runs: ask — it proposes register, attach, test.

Some pages pre-write a question (Settings → Connectors passes the pasted URL).

**Never paste keys, tokens or passwords into chat.** Use the dashboard forms.

## Answers

The actual screen, button or field. One right next step. Unknown? It says so.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#ask-agent)
