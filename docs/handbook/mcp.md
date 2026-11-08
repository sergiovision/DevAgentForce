# The MCP server — drive the platform from your coding CLI

**Pro.** Knowledge base and task lane for any MCP agent — Claude Code, Codex, Antigravity, Ask Agent. Same worker as the dashboard; answers match.

- **stdio** beside your CLI — repo detected from the launch folder.
- **Remote HTTP** — Agent Peer credential, scoped to that peer's repos.

## Tools

- **Ground** — `wake_digest` first (identity, key facts, recent decisions); `task_scope` (read vs write, checkout state, index freshness).
- **Memory** — `memory_search` over notes, facts, decisions, relationships. `kind=transcript` adds verbatim prior attempts (off by default — check before an expensive retry).
- **Code** — `repo_map`, `code_search`, `doc_search`, `corpus_search_all` (all repos).
- **Write** — `memory_save` (content, `kind` note/fact/decision, `topic`; redacted). `memory_feedback` — helpful, not helpful, stale, wrong; reorders, never deletes.
- **Tasks** — `task_options`, `task_create`, `task_run`, `task_list`, `task_status`, `task_output`, `task_cancel`, `skill_list`, `backlog_read`.
- **Operate** — `task_diff`, `log_tail` (worker/web/task, redacted), `analytics_summary`, `repo_list`, `template_list`, `schedule_list`. Writes: `task_continue`, `task_retry`, `idea_create`, `template_create`, `mcp_server_add` (panel only: add and test an external MCP server).
- **Deployment** — `setup_scan`, `vault_status`, `session_search` (earlier sessions), `propose_action` (approve before it runs).

In the panel every write is a proposal.

## Know this

- **Writes are searchable at once — and only hints.** No review, no verification, no expiry. Check the repo before relying on one.
- **Empty answers say why.** `no_match` = nothing stored. `unavailable` = search could not run (embeddings off, DB error). Never padded.

**"Endpoint not found"** — worker down, free build, or repo never indexed. Start the worker; check `corpus_stats`. Creating tasks also needs the **dashboard** — the worker never writes the queue.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#mcp)
