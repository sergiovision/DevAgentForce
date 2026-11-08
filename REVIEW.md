# REVIEW — DevAgentForce public docs folder

For the owner, before publishing to `github.com/sergiovision/DevAgentForce` by hand. **Nothing was published.** There is no `git init`, no remote, no push, no PR and no GitHub API call. Everything is uncommitted in the private repo as `?? DevAgentForce/`.

## Before you publish (TODO)

1. **Demo media.** README links the overview-video poster to the product page. Add a GIF or YouTube link at the `<!-- TODO: demo GIF + YouTube link -->` marker if wanted.
2. **Security email.** Replace `security@<TODO>` in `SECURITY.md`.
3. **FinCore link.** Check the URL in `_profile/README.md` (assumed `github.com/sergiovision/FinCore`) and its one-line description. The star count (48) is taken from the task brief.
4. **Profile README.** Move `_profile/README.md` to the `sergiovision/sergiovision` repo, then delete `_profile/` from this folder.
5. **Discussions.** Enable GitHub Discussions with the categories **Q&A** (`q-a`) and **Ideas** (`ideas`). The issue `config.yml` and the discussion templates point at them.
6. **Logo-free hero art.** The two private hero images show vendor logos on the horses, so they were not copied. [`assets/art/ART-TODO.md`](assets/art/ART-TODO.md) specifies the two replacements (same scenes, no vendor logos).
7. **docs CI.** markdownlint runs with `continue-on-error` (advisory) until a first clean pass. lychee and gitleaks are blocking. Config: `.github/markdownlint.yml`.

## Source inconsistencies found (fix in the private repo)

- **Sessions observatory edition.** The capitaltools docs page (Pro section) and `docs/session-observatory.md` list the viewer as Free. The capitaltools product catalogue FAQ and the brief list it as Pro. The public docs say **Pro** throughout.
- **Ask Agent tools edition.** The private README and handbook say the tools are Free in every edition. The capitaltools docs page and the brief say Pro. The public docs say **Free chat, Pro tools**.
- **Local Git flows.** `docs/assistant/repos.md` says only Untracked and Patch are allowed on a local folder. `docs/gitops.md` and the capitaltools product catalogue say all four flows work. The public use cases follow `gitops.md`/the capitaltools product catalogue. The handbook copy keeps the source wording.
- **Pi isolation advice.** The capitaltools product catalogue still says "use Docker for untrusted repositories", but Docker was removed. The public FAQ gives the current advice: an OS sandbox on macOS/Linux, or a disposable VM.
- **PostgreSQL version.** The private README says 16/17. Installers bundle 18.x. The public tech stack says "16+ (installers bundle 18.x)".

## Sources used per page

| Page(s) | Sources |
|---|---|
| `README.md` | `README.md` (pitch, Why, Quick Start, Roadmap), `README.PRO.md` edition table, the capitaltools product catalogue FAQ (edition split), the capitaltools portfolio data `hero` |
| `CHANGELOG.md` | the capitaltools changelog data (DevAgentForce 2.0.7 to 2.0.232 entries), `version.json` |
| `LICENSE`, `TRADEMARKS.md`, `SECURITY.md`, `CONTRIBUTING.md` | Written new |
| `docs/getting-started.md` | `docs/assistant/getting-started.md`, `native.md`, `desktop.md`, `updating.md`, README Quick Start, `config/.env.example` (key names only, values replaced by placeholders) |
| `docs/editions.md` | the capitaltools product catalogue FAQ "what does Free include", the capitaltools docs page `#pro`, `README.PRO.md` edition table |
| `docs/faq.md` | `docs/assistant/faq*.md` (5 pages), the capitaltools product catalogue FAQ (no prices, no trial/seat/activation mechanics) |
| `docs/handbook/*` (29 pages) | Copies of `docs/assistant/*.md`, sanitized (see below), each with a footer link to the matching capitaltools.app anchor. Index in `00-manifest.json` order |
| `docs/features/*` (20 pages) | One rewrite per topic doc: `task-types`, `agent-backends`, `workflows`, `review-loop`, `skills` + `artifacts`, `gitops`, `cross-repo`, `memory-kb`, `mcp-control` + `mcp-integrations`, `secrets-store` + `auth-and-security`, `ideas-backlog`, `ask-agent`, `session-observatory`, `messaging`, `script-tasks`, `a2a-gateway` + `crew-migration`, `worker-fleet`, `desktop`, `backup-restore`; plus README / README.PRO sections and matching handbook pages |
| `docs/engineering/*` (10 pages) | `README.md` (Architecture, Design Decisions 1–5, Tech Stack), `docs/adr/0001–0003`, `CLAUDE.md` invariants (rewritten, not quoted), `docs/testing.md`, `docs/features.md` (area counts), `docs/secrets-store.md`, `docs/pro-architecture.md` (capability level), `docs/messaging.md`, `docs/claude-code-shared-memory.md`, `docs/desktop.md`. Table names and foreign keys from the migration were used for the ER diagram only, and the coding-run phase order from the worker code |
| `use-cases/*` | README, README.PRO, `docs/workflows.md`, `review-loop.md`, `gitops.md`, `artifacts.md`, `skills.md`, `messaging.md`, `agent-backends.md`, `script-tasks.md`, handbook. Use case 07 uses facts only from `docs/handoff/T1-T5-USE-CASES.md`, rewritten generically |
| `_profile/README.md` | the capitaltools portfolio data `hero`, `skillGroups`, `social` |
| `assets/` | `assets/logo/DevAgentForceLogo.jpg`, `DevAgentForceIcon.jpg`; `art/ART-TODO.md` written new. Screenshots are linked from capitaltools.app, not copied |

## Sanitized or deliberately excluded

- **Never-publish sources.** None were read into public pages: monetization, marketing analyses, competitor gap docs, licensing, Jenkins, nginx-tailscale, db-schema audit, refactor, handoffs (except the use-case facts), Plan*/RLM, store, LICENSE.PRO, backups/data/logs.
- **Vendor-logo art.** `BeforeDevAgentForce.jpg` and `WithDevAgentForce.jpg` were not copied (they show Claude/Gemini/ChatGPT logos). See `assets/art/ART-TODO.md`.
- **Handbook changes.**
  - `assistant.md` was the assistant's own instruction text. It is rewritten as a user-facing page, *About the Ask Agent assistant*, with no prompt text, script paths or action keys.
  - `pro.md` "Getting Pro": the trial-key, signed-token and re-verification mechanics are reduced to trial, activate, offline activation and lapse-to-free. The reality-gate "0–100 / threshold" scoring is reduced to capability level.
  - `faq-restore.md`: "share one licence seat" became "run only one at a time".
  - `native.md`: the private-network CIDR is removed ("from your Tailscale network only").
  - `overview.md`, `faq-setup.md`, `mcp.md`: "this platform / this panel / this assistant" now name DevAgentForce / the Ask Agent panel.
  - `workspace.md`: the example `@fincore` is now `@backend`, so the page does not name another project.
  - Kept on purpose, because users need them: user-facing CLI commands (`scripts/start.sh`, `devagentforce migrate` …), env var *names* users set (`ENABLE_LOGIN_PAGE`, `GITHUB_TOKEN`, `INTERNAL_API_TOKEN`), user-visible file locations (`~/.devagentforce/vault.key` for backups), public API route prefixes in `access.md`, the `.daf/review-rules` folder.
- **Pro features.** Capability level only. No reality-gate weights or thresholds, review confidence cutoffs, budget percentages, memory scoring, chunk sizes or preflight rule counts.
- **Engineering pages.** No function, package or file names, no advisory-lock number, no masking placeholder tokens, no SQL or columns (the ER diagram has names and cardinalities only).
- **Other.** Prices, the donation wallet, licensing/seat/token mechanics, specific model version names (they go stale), private hosts and IPs, Jenkins, and the owner's other private projects.

## Screenshots

There is no `assets/screenshots/` folder, on purpose. The local `assets/*.png` copies show private data, so all of them were excluded. Images are linked from the capitaltools.app product carousel instead:

`https://capitaltools.app/devagentforce/<name>.png`

The 12 names are: dashboard, tasks, viewtask, sessions, templates, skills, ideas, repos, secrets, crew, settings, logs. The README also links the overview video poster at `https://capitaltools.app/devagentforce/video/devagentforce-overview-poster.jpg`. Every URL returned HTTP 200 when this folder was built.

**Check these images on the live site.** Some of them show the same private data the local copies had, so it is already public:

| Image | What it shows |
|---|---|
| `crew.png` | Private-network IPs and a private hostname |
| `logs.png` | Hostname, the Telegram bot name, the key fingerprint |
| `viewtask.png` | Internal source paths |
| `tasks.png`, `ideas.png` | Internal task titles |

Swap the files on capitaltools.app and this repo picks up the new versions automatically. If you'd rather have local copies, add clean PNGs under `assets/screenshots/` and point the README at them.

## Rewrite pass

**Added for tech leaders and hiring managers.** Eleven more diagrams in `docs/engineering/`:

| Page | Added |
|---|---|
| `README.md` | Mindmap of the engineering areas |
| `design-decisions.md` | Decision map, kernel / seams / modules diagram, retry-and-failover decision tree |
| `reliability.md` | Job claim / heartbeat / panic / shutdown sequence, admission flowchart |
| `testing-strategy.md` | Gate pipeline, pie chart of feature IDs by area |
| `tech-stack.md` | Deployment topologies (native, desktop, cloud VM) |
| `security-model.md` | Secrets resolution order, local-repo safety flow |

Every page was shortened and rephrased in a terse, checklist style: short declarative lines, steps, tables, no filler. Facts, links, Free/Pro badges and diagrams were kept. Line counts: handbook 1905 → 1068, features 1168 → 995 (about 38% fewer bytes), engineering 885 → 709 (about 49% fewer bytes), use cases + FAQ 913 → 563.

## Checks

- **Mermaid.** All **45** diagrams were extracted and rendered again in the final pass with `@mermaid-js/mermaid-cli` (via `npx -y`). Result: **45 ok, 0 failed**. The required set is present:
  - README flowchart
  - architecture context + container
  - task-lifecycle sequence + state
  - data-model erDiagram
  - one flowchart per use case (7)
  - security-model trust-boundary flowchart
- **Acceptance check 1.** Every file in the structure exists, including `assets/art/ART-TODO.md`. `docs/handbook/` has 29 pages plus `README.md`. The one deliberate exception is `assets/screenshots/` (see Screenshots).
- **Acceptance check 2** (`find DevAgentForce -type f | grep -Ev '\.(md|ya?ml|png|jpe?g|gif|svg)$|/LICENSE$'`):
  ```text
  (no output)
  ```
- **Acceptance check 3** (leak grep from the brief):
  ```text
  (no output)
  ```
  No exceptions were needed. An extended sweep also looked for: hostnames, Jenkins, prices, internal function names, the lock number, `/Users/`, `C:\dev`, and the bot name. Its only hits are the user-facing items listed as kept above.
- **Acceptance check 4.** `BeforeDevAgentForce.jpg` and `WithDevAgentForce.jpg` are absent.
- **Acceptance check 5** (every relative Markdown link and `src=` resolves; fenced code blocks skipped):
  ```text
  broken: 0
  ```
- **Acceptance check 6** (`git status --porcelain`):
  ```text
   M version.json      (your own edit, outside this task)
  ?? DevAgentForce/
  ```
- **Acceptance check 7.** No `.git` inside `DevAgentForce/`, no remote added, nothing pushed. The private repo's existing `origin` was not touched.

## Files created

```text
.github/DISCUSSION_TEMPLATE/ideas.yml
.github/DISCUSSION_TEMPLATE/q-a.yml
.github/ISSUE_TEMPLATE/bug_report.yml
.github/ISSUE_TEMPLATE/config.yml
.github/ISSUE_TEMPLATE/feature_request.yml
.github/markdownlint.yml
.github/workflows/docs-ci.yml
CHANGELOG.md
CONTRIBUTING.md
LICENSE
README.md
REVIEW.md
SECURITY.md
TRADEMARKS.md
_profile/README.md
assets/art/ART-TODO.md
assets/logo/DevAgentForceIcon.jpg
assets/logo/DevAgentForceLogo.jpg
docs/README.md
docs/editions.md
docs/engineering/README.md
docs/engineering/architecture.md
docs/engineering/context-economy.md
docs/engineering/data-model.md
docs/engineering/design-decisions.md
docs/engineering/reliability.md
docs/engineering/security-model.md
docs/engineering/task-lifecycle.md
docs/engineering/tech-stack.md
docs/engineering/testing-strategy.md
docs/faq.md
docs/features/README.md
docs/features/a2a-gateway.md
docs/features/agent-backends.md
docs/features/ask-agent.md
docs/features/backup-restore.md
docs/features/cross-repo.md
docs/features/desktop-app.md
docs/features/git-providers.md
docs/features/ideas-backlog.md
docs/features/mcp.md
docs/features/memory-and-knowledge.md
docs/features/messaging-and-telegram.md
docs/features/pipeline-and-tasks.md
docs/features/review-loop.md
docs/features/schedules-and-scripts.md
docs/features/secrets-vault.md
docs/features/sessions-observatory.md
docs/features/skills-and-artifacts.md
docs/features/worker-fleet.md
docs/features/workflows.md
docs/getting-started.md
docs/handbook/README.md
docs/handbook/access.md
docs/handbook/assistant.md
docs/handbook/desktop.md
docs/handbook/faq-queue.md
docs/handbook/faq-restore.md
docs/handbook/faq-secrets.md
docs/handbook/faq-setup.md
docs/handbook/faq.md
docs/handbook/getting-started.md
docs/handbook/integrations.md
docs/handbook/mcp.md
docs/handbook/memory.md
docs/handbook/native.md
docs/handbook/overview.md
docs/handbook/pro.md
docs/handbook/repos.md
docs/handbook/secrets.md
docs/handbook/sessions.md
docs/handbook/settings.md
docs/handbook/skills.md
docs/handbook/task-finish.md
docs/handbook/task-types.md
docs/handbook/tasks.md
docs/handbook/templates-ideas.md
docs/handbook/troubleshooting.md
docs/handbook/updating.md
docs/handbook/vendors.md
docs/handbook/workflows.md
docs/handbook/workspace.md
use-cases/01-ticket-to-verified-pr.md
use-cases/02-plan-then-implement.md
use-cases/03-overnight-multi-vendor-batch.md
use-cases/04-local-repo-no-remote.md
use-cases/05-pre-ship-review-loop.md
use-cases/06-research-with-artifacts.md
use-cases/07-scheduled-skills-job-search.md
use-cases/README.md
```
