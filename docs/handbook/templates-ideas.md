# Templates, ideas and schedules

Save the repeat task. Grow ideas into tasks. Run work on a clock.

## Templates (`/templates`)

Preset: description, criteria, type, git flow, vendor/model, backup, billing, max turns, `/task-verify`. Pick on New Task; edit what differs. For anything typed twice — release checklists, dependency bumps, audits.

## Ideas/Backlog (`/ideas`)

Nested notes tree.
- **Expand / Decompose** (Pro) — system LLM splits an item into a sibling folder (same title) of atomic steps, each scored 0–100.
- **Roll up** — subtree summary into the parent.
- **Drag** — *between* rows to place, *onto* a folder to file. Order saved. Keyboard drag works; F2 renames; filter dims non-matches.
- **Repository binding** — a folder's repo applies to everything inside, unless overridden.
- **Multi-select** — Ctrl/Cmd-click, Shift-click range. **Delete** shows the count; folders take contents. Always confirms.
- **Counts** — pill = direct items; hover = total with sub-folders.
- **Resize** — drag the divider; remembered per browser; stacks below tablet width.

**Convert to Task** — the only exit. Title, body, inherited repo carry over; type from the form (coding, or `research` for a plan). No "Convert to Plan" — the DevPlan skill is unchanged (`POST /internal/generate-plan`).

`@Backlog: Root/Payments` in a description hands the agent a whole folder. See *Working across more than one repository*.

Loop: dump → decompose → prune → promote. Pro: Azure DevOps connector files items straight into a folder.

## Jobs (Settings → Jobs)

Cron re-queue of an existing task — nightly checks, weekly sweeps. Run now or stop mid-flight. **Runs**: status, time, summary, `RESULT.md`. Invalid schedules refused with the reason.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#ideas)
