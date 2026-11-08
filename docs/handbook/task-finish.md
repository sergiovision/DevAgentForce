# Images, files, review loop and follow-up actions

Attach evidence, chain the next step, review before delivery.

## Images and files

Paste or drop a screenshot into description or criteria, or **Add file(s)**. Text is inlined; images and documents (PDF, Word, …, ≤ 10 MB) attach to the task's folder — never base64. Codex gets an image input; Claude and Antigravity the folder. PDF/Word get a `.txt` copy when possible.

## Run action on completion

On New Task and Quick Task:
- **/task-verify** — coding default. Build/test/lint before shipping; failures go back. *No action* disables.
- **A skill** — child `skill` task, default or custom parameters. Review skills (`code-review`) see exactly the parent's changes (branch, or local diff range).
- **A script task** — runs that command, detached.
- **A pending task** — enqueues another (never itself).

**Trigger**: *On success* (default), *On failure*, *Always*. A failing action never fails its parent.

## Review loop (Pro, coding)

**Review the changes before delivering**: after verify, a reviewer reads the changes; the task's agent fixes or declines; re-verify; repeat until clean or a limit. Then normal delivery.

- **Reviewer vendor / model** — blank = task's. On failure, once to the backup pair.
- **Max rounds** 1–10 (default 4). No retries used; cost and time hit the budget.
- From round 3, only *blocking* findings (wrong code, broken contract, leaked secret, missing tests) get fixed.
- **Filtered**, never sent: no quoted evidence, confidence < 80, duplicates, declined.
- Repo rules: `.daf/review-rules/*.md`.

Shows `verifying`, ends `test`. Limit hit: **Review: needs you** with open findings. Remote *commit* flow with an open blocker: nothing pushed; **Continue** resumes the kept worktree. PR body gets a Review section.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#attachments)
