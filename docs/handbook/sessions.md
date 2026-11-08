# Sessions

Every coding-CLI session on the worker host, live — yours too. **Sessions** (`/sessions`); search and Scripts need **Pro**.

## The list

Tabs per active vendor — **Claude**, **Gemini**, **Codex**, **Pi** — read each CLI's transcripts. Counter: *"N live · M on this host"*. Filter box, **Live** checkbox.

- Dot: green pulsing busy · teal live idle · amber idle, process gone · grey finished. Plus label, idle time.
- Badge: **agent** (task), **ask agent**, **console** (your terminal), **external**; task key, status colour, repo. `…` opens the task.
- Matched by session id — claimed before Claude spawns; Codex and Gemini report at run end. Retries and failovers fold into one row.
- **Search** (toolbar) looks *inside* all transcripts; the filter only matches label, repo, key. Click a hit for a highlighted view. Bounded; says when it stopped early.

## The transcript

Tails live on the right; drag the divider.
- Header: label, task key, branch, turns, tokens, updated, session id (copy — for `--resume` and greps).
- Cut events: **show full** (re-read from disk), **save as file**.
- **Delete** (Claude, Gemini): permanent, confirms, blocked while live. Codex read-only.

## Steering

A task's session gets a chat box:
- **Approve plan / Reject** — at the plan gate.
- **Approve / Yes**, **Reject / No** — side-effect question.
- **Send** (Enter) — instruction as operator.
- **Stop** — separate control. Cancels; edits on disk stay.

**Quick Task** (green) → *Start Interactive Task*: repo, vendor, model, description. Interactive, no push, no PR. Local: uncommitted edits in your checkout; else `agent/<task-key>` in the worktree. Same transcript as the task's **Task Log**.

## Empty tab

Reads `~/.claude/projects`, `~/.gemini`, `$CODEX_HOME/sessions`. A missing-directory banner: CLI never ran here, or the worker cannot see its home. Text is capped and redacted.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#sessions)
