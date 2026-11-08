# Task types

Set at creation, **never changed**. Picks the runner and the form fields.

| Type | Repo | Does | Output |
|---|---|---|---|
| `coding` | required | Worktree → agent → verifier → PR. Default | PR / patch |
| `test` | required | Agent runs tests (e.g. "suite on branch X, what broke"); criteria become *"Which tests must pass"* | Task Log |
| `script` | required | Agent runs a command and reports | Task Log |
| `skill` | optional | SKILL.md in a scratch dir. Never commits or pushes; with a repo, runs inside it (read-only in spirit) | `docs/skill-work/<KEY>/RESULT.md` + Task Log |
| `research` | optional | Description is the prompt; questions, comparisons. No code changes | Task Log + `docs/skill-work/<KEY>/RESULT.md` |

`test` and `script` skip the worker verifier; the agent tests its own work.

## Switches

- **`/task-verify`** (coding default) — build/test/lint before commit or PR; failures go back. *No action* for docs/config. Hidden for `test`/`script`.
- **Max turns** — `-1` = unlimited. Hitting it often = under-specified, not under-budgeted.
- **Mode: interactive** (Pro) — plan first, wait for approval.

Templates set the type too.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#tasks)
