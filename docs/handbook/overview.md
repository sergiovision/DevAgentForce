# What DevAgentForce is

Describe a job. A coding agent (Claude Code, Codex, Antigravity, Pi) does it in an isolated git worktree. Verified, then delivered as a pull request.

## The pipeline

1. **Create a task** — title, description, repo.
2. **Queue** — PostgreSQL-backed; survives restarts. Parallel up to worker concurrency, even on one remote repo. Exclusive lock only for shared-checkout changes: local *patch* or any *direct commit*.
3. **Agent** — private worktree; your copy untouched. Gets a repo map, prior context, acceptance criteria.
4. **Verifier** — build / test / lint. Failures return as classified errors for a targeted retry.
5. **Delivery** — PR or patch, per git flow.

`pending → queued → running → verifying` → `test` (success, awaiting review), `failed` or `cancelled`.

## Screens

| Screen | For |
|---|---|
| **Dashboard** (`/`) | Worker controls, live sessions (Pro), running agents, cost/duration/turns/tokens analytics |
| **Tasks** (`/tasks`) | Backlog; grid or pipeline board |
| **Task detail** (`/tasks/{id}`) | Timeline, runs, logs, agent settings, patches |
| **Templates** (`/templates`) | Task presets |
| **Skills** (`/skills`) | SKILL.md procedures, libraries, usage |
| **Ideas/Backlog** (`/ideas`) | Idea tree; folders bind to repos, nodes become tasks |
| **Settings → Jobs** | Cron re-runs |
| **Repos** (`/repos`) | Repositories |
| **Settings** (`/settings`) | Queue, system LLM, `.env` editor |
| **Secrets** (`/secrets`) | Encrypted store, import from `.env` |
| **Logs** (`/logs`) | Live worker and web output |
| **Crew** (`/workers`, Pro) | Other instances: liveness, pause/resume |
| **Sessions** (`/sessions`) | Live CLI transcripts; Pro search |
| **Connectors** (Settings, Pro) | Tracker items → pending tasks or ideas |

⌘/Ctrl+K — command palette (last row asks Ask Agent). ⌘/Ctrl+J — Ask Agent. `?` — all shortcuts.

## Processes

- **web** — dashboard, port 3200. Only queue writer.
- **worker** — port 8000. Runs agents, verifies, talks to Gitea/GitHub.
- **PostgreSQL** — state, events, Pro memory/vectors.

Both processes must run. Updates stream over WebSocket — no refresh.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#overview)
