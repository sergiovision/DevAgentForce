# Repositories and git flows

**Repos** (`/repos`): where code lives, how to build and test it, agent defaults.

## Providers

| Provider | Setup |
|---|---|
| **Gitea** | Clone URL + token; Gitea API PRs |
| **GitHub** | `github.com` URL; `Bearer` token |
| **Azure DevOps** | `dev.azure.com` / `*.visualstudio.com`; PAT with *Code (Read & Write)*; org, project, repo from URL |
| **Local Git** | Existing folder on the worker. No clone, no remote |

- Per-repo token beats global. Never cross providers — a Gitea token on GitHub (*"Invalid username or token"*) is refused.
- Azure PAT per repo (`vault:<ref>` ok) or `AZURE_DEVOPS_TOKEN`. A dependent folder needs its own repo entry for Branch + PR.
- Local Git: path in **Local Root Folder**. Never pushed, reset or cleaned. *Untracked* and *Patch* only.

## Settings

- **Build / Test / Lint / Pre** — verifier commands. Empty = skipped.
- **Default branch**, **max retries**, **timeout**, **CLAUDE.md path**.
- **Deploy command** — not a verifier step; runs later in the real checkout, may restart the system. No per-task auto-run switch any more — nothing restarts by surprise. Repos with it already on keep deploying.
- **Dependent Repositories / Folders** — see *Working across more than one repository*.

## Git flows

| Flow | Result |
|---|---|
| **Untracked** (default) | Edits in a worktree. No branch, commit, push, PR |
| **Direct Commit** | Squash-merge to default branch |
| **Patch** | Commits on local `agent/{task_key}` → `combined.mbox` for `git am`. Not pushed |
| **Branch + PR** | Push `agent/{task_key}`, open PR |

Local repo: *Untracked* edits your folder uncommitted; *Patch* commits on an `agent/…` branch, then restores yours.

## Isolation and tools

- One bare mirror, one worktree per task. No collisions; your checkout is safe. Worktrees reset after — local folders left alone.
- **Refresh Git** — re-fetch (local: revalidate). **Architecture diagram** — Mermaid module map, no LLM. **Reindex** — semantic index (Pro).

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#repos)
