# Workflows (Pro)

Ordered **steps** from a **workflow template**. Each step is its own task.

## Run

- Start: **Workflow** task type, or ask me. Watch: `/workflows`. Templates: `/templates?type=workflow`.
- A step's task page shows the workflow, that step marked.
- **Remove** deletes a non-running workflow; step tasks stay.

## Built-ins

Edit in place or **Duplicate**. Edits survive updates. No rename, no delete.
- `feature` — Plan (PLAN.md, sign-off) → Implement.
- `bugfix` — same; plan names a failing test.
- `multi-review` — three parallel reviews → one merged PLAN.md → Implement with one review round. Scope (paths, ref, focus) goes in the description.

## Step fields

- `key` (lowercase, unique), `label`, `kind`, `signoff`: `always`, `never`, `if_option` (waits unless auto-approve).
- `light` — runs an enabled `skill`, writes `output: {kind, file}`.
  - `vendors: ["anthropic", "google", "openai", "pi"]` (2–4) — parallel; next step gets all outputs.
  - `models: {"pi": "provider/id"}` — `pi` needs one, and Pi on in Settings → Vendors.
- `coding` — implements `inputs`. `allowlist_from` limits files to a plan's `files_to_touch`. `review_rounds` 1–10.
- `condition` — `rules`, `then`, `else`. Loops need `max_iterations`.
- `inputs` — earlier steps' latest output, pinned.
- `contract` — checks a light step's file: `sections`, `front_matter`, `word_cap`, `max_fence_lines`.

## By asking

I use `workflow_template_list`, `workflow_template_create` and `workflow_start` (title, description, template, `auto_approve_plan`, `git_flow`). Each is a card; nothing runs until you click Run. Any install, desktop too — no source needed. Errors name the step to fix.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#pro)
