# FAQ

Short answers. Deeper: stuck tasks, setup, secrets, backup.

**API key needed?** Only for *API Platform*. *Max (subscription)* strips it; the CLI uses your login (`claude login`, `codex login`, Google OAuth for `agy`) — **on the worker machine**.

**Which vendor first?** The CLI you have logged in. Add a **backup vendor** for rate-limit failover.

**Task created, nothing happened.** Web writes the queue, worker reads it. Web was down → **Re-run**. Worker down → stays `queued`. Queue paused? Settings or Telegram `/status`.

**Without Gitea or GitHub?** Yes — **Local Git**, any existing clone. No push, no PR: a local `agent/<task-key>` branch with patches, or uncommitted edits.

**Failed with little agent work.** A gate, named on the detail page: preflight, budget, rejected plan, reality-gate abstain. Fix, then **Continue**. No `blocked` state — side-effect waits show `pending`.

**Database change ignored.** Read once when the pool opens. Restart.

**Need Pro?** No. Pro features become no-ops. A licence unlocks reality gate, memory KB, plan gate, budget ceilings, PR preflight, patch export — dormant in release builds. Ask Agent, its tools and fixes are free, no System LLM needed.

**Cost?** Dashboard: total and per PR. Task page: per task. Max billing reports zero; *Avg Tokens per Task* (input incl. cache reads, output) still shows size.

**Requirements?** Native installer (`install.sh` / `install.ps1`) needs only PostgreSQL, and can install one. See *Native install*.

**Full docs?** https://capitaltools.app/devagentforce/docs — or the book icon here. `/faq` lists common fixes.

**Logs?** `/logs` live; agent transcript on the task page; disk: `logs/worker.log`, `logs/web.log`.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#faq)
