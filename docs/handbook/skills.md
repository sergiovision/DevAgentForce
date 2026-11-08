# Skills

Reusable procedures: a folder with `SKILL.md` (frontmatter + Markdown) and optional files. Page: **Skills**.

## Make

- **New skill** — name (lowercase → `/name`), description, optional **parameters** (name, required, default), instructions. Saved as `skills/<name>/SKILL.md`.
- **Import** `SKILL.md`, `.zip`, `.skill`. **Export** a zip.
- **Libraries** — folder, git repo, archive URL + sha256, catalogue, prompt-only catalogue. *Sync* shows updates; *Update*/*Rollback* move the pin; **Discover** browses. Read-only — **Duplicate** to edit.
- Security scan: *blocked* never installs; *warn* starts disabled.
- **Save as skill…** on a finished task — System LLM drafts, editor opens, nothing saved until Save. Offered once after three similar successes.

## Presets

Badge *preset*, read-only — **Duplicate** to edit.
- `/grill-me` — interviews a plan until settled, writes a ready-to-run task.
- `tdd`, `diagnosing-bugs`, `code-review`, `writing-for-agents`.
- `senior-code` — smallest complete change; `target=` slims existing code.
- `webhook` — runs every webhook trigger delivery (Pro, *Triggers* on its card). *plan* answers the implied task; *act* does it in a coding task.
- `/skills-index` — every skill and when to use it. Regenerated each sync.

## Use

1. **Call** — a `skill` task. *Run Skill* opens New Task pre-picked; fill Parameters. Missing required value: agent stops, never guesses. *Parameter defaults* (Skills settings) pre-fill; task > yours > skill's.
2. **Attach** — *Attached skills*, any type but script. Added to the prompt. Missing or disabled **fails the task**.
3. **Catalog** — *Skill catalog* on (Settings): each run sees a one-line list of its repo's allowed skills (repo *Skills available to agents*: inherit / none / all / list). Loaded only on match. **User-invoked** skills never listed.

- Dependencies ("Skill tool with `tdd`", `requires:`) install too.
- Results: Task Log + `SKILL_WORK_DIR/<KEY>/RESULT.md` (default `docs/skill-work/<KEY>/` under the install root, never in the task repo).
- Only **git-capable** skills may commit, branch, merge or rebase. Never push.

## Usage and versions

- Per skill: runs, success rate, median tokens, use (called, attached, dependency, auto).
- **Details**: origin, scan report, diff, trigger eval, publish checklist.
- Runs record a fingerprint; **Continue** after an edit makes the agent reload.

## In this panel

`/skill list [query]` · `/skill show <name>` · `/skill run <name> key=value` (prefills New Task, submits nothing). Pro: ask me to *write* or *change* a skill — I draft, you approve on a card.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#skills)
