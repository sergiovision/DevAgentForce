# Working with tasks

Describe the job, pick the agent, watch it run.

## Create

**Tasks → New Task** (`/tasks/new`) or *New Task* on the dashboard.

| Field | Notes |
|---|---|
| **Title** | Short. Becomes PR title and task key |
| **Task type** | Fixed at creation. See *Task types* |
| **Repository** | Required: `coding`/`test`/`script`. Optional: `skill`/`research` |
| **Description** | The agent's prompt. Name files and behaviour |
| **Acceptance criteria** | Done condition. Read by verifier and retry loop |
| **Git flow** | Branch + PR, patch, direct commit, untracked (default — nothing leaves the worktree) |
| **Vendor / Model / Billing** | Which CLI, how paid |
| **Priority** | 1 critical, 2 high, 3 medium (default), 4 low |
| **Run action on completion** | Verify, or a follow-up action |

**Fill Task** — system LLM expands one line into a full task. **Templates** pre-fill every field.

**Task key** — e.g. `DEV-123`, `MCP-FIX-LOGIN`. Names the branch (`agent/{task_key}`), log file, patch directory. Telegram and API take it as argument.

## Statuses

| Status | Meaning |
|---|---|
| `pending` | Not on the queue, or awaiting your decision (plan, side-effect gate) |
| `queued` | Waiting for a worker / repo lock |
| `running` | Agent working |
| `verifying` | Build/test/lint |
| `test` | Succeeded, awaiting review |
| `failed` | Retries exhausted, or stopped on purpose (budget, preflight, abstain, refused plan) |
| `cancelled` | You stopped it |

## Controls (task detail page)

- **Run / Re-run** — back on the queue.
- **Cancel** — stop running or verifying.
- **Continue** — resume with session, branch and conversation intact. For an on-track agent out of turns.
- **Compact** — history → brief, fresh conversation. For context full of dead ends.

Page shows the **event timeline** (retries, classified errors, verifications), **runs** (cost, turns) and live **Task Log**.

## Dictate

**Dictate** beside the description (plain http: **Dictate audio file**).
- Greyed phrase at the cursor; finished phrases are typed in. **Stop** or submit — pending speech kept.
- Engine: Google Gemini (`GEMINI_API_KEY`) or local Whisper (`DICTATION_STT_URL`).
- Live needs HTTPS or localhost. Plain http records a clip (phone recorder or file).

## Ordering

Priority, then age, several at once. Different vendors share a repo in parallel. Same-vendor tasks and local-checkout commits wait for the repo lock.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#tasks)
