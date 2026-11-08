# Working across more than one repository

Three different tools. Mixing them up causes "why couldn't the agent edit that file?"

| I want the agent to… | Use |
|---|---|
| know another repo's shape | `@repo_name` in the task text |
| change files in another checkout | Dependent Repositories / Folders on the repo |
| work a list from the tree | `@Backlog: path` in the task text |

## `@repo_name` — read-only

`@backend` in title, description or criteria gives the agent that repo's name, id, branch, worker path and symbol-map lanes. "Match the API shape in `@backend`."
- Only **active repository** names match — emails and `@decorator`s are safe.
- Up to 4. Unresolved names logged in task events.
- A pointer, not a grant.

## Dependent repositories and folders — writable

Repo form (`/repos`): **Dependent Repositories** (registered, by name), **Dependent Folders** (absolute worker paths). The agent may **read, edit and commit** there — fix a backend type and the frontend in one task.
- **Never pushed.** Local commits on the current branch; no branch, PR, reset or clean.
- **The repo owns the grant.** No task field widens it — webhooks, imports and peers stay out.
- Preflight and patch export cover the own repo only; the agent lists dependent dirs it touched.
- Each dir locked per task.
- Gemini/Antigravity has no flag — the task logs the grant as not applied.

## `@Backlog: Folder/Path`

`@Backlog: Root/Platform/Payments` resolves the **Ideas/Backlog** folder, its bound repo (own or inherited), and hands over every item. Unresolvable paths are reported, not guessed.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#repos)
