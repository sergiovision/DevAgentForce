# Changelog

Full dated history: **[capitaltools.app/devagentforce/changelog](https://capitaltools.app/devagentforce/changelog)**.

## 2.0 — current

Rebuilt from the ground up. Go worker. Next.js 15 dashboard. PostgreSQL with pgvector. Native installers and a desktop app for Linux, macOS and Windows.

**Agents**
- Four vendors: Claude Code, Codex, Antigravity, Pi.
- Pi opens any OpenAI-compatible endpoint — and local models via Ollama, LM Studio, llama.cpp, vLLM.
- Switch any vendor on or off.
- `-latest` aliases always run the newest model.
- Context overflow? Compacts once, retries free.

**Workflows and review** — Pro
- Plan → approve → implement. Plan in `PLAN.md`, code in a PR.
- Custom workflows: conditions, routing, review loops, sign-offs, USD budget.
- One review step across two or three vendors.
- Evidence-only findings. Your rules in `.daf/review-rules`.
- Artifacts page for `RESULT.md` and `PLAN.md`.

**Operations**
- Schedules keep per-run history.
- `{{placeholders}}` in templates become required inputs.
- Update: re-run the installer. A notice shows the command.
- Desktop app. Bundled database. Dictation. Nine languages.
- Bug reports from the Logs page, diagnostics attached.

**Security**
- Invisible characters stripped. Untrusted text marked as data.
- New or changed MCP write tools held for review.

[Editions](docs/editions.md) · [Features](docs/features/README.md)
