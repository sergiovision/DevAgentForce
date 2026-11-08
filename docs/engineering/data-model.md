# Data model

One PostgreSQL database: records, job queue, event stream, embeddings. One migration file, about fifty-six tables. Below: the 23 core entities and their relationships.

```mermaid
erDiagram
  repos ||--o{ tasks : "hosts"
  tasks ||--o{ task_runs : "attempted as"
  tasks ||--o{ task_events : "emits"
  task_runs ||--o{ task_events : "emits"
  task_runs ||--o{ review_findings : "reviewed in"
  tasks |o--o{ tasks : "follow-up script"

  skill_sources ||--o{ skills : "provides"
  skills |o--o{ tasks : "called by"
  skills ||--o{ skill_invocations : "invoked as"
  task_runs ||--o{ skill_invocations : "records"
  skills |o--o{ task_templates : "preset in"

  tasks ||--o{ schedules : "re-run by"
  schedules ||--o{ schedule_runs : "fires"
  tasks |o--o{ schedule_runs : "executes"

  repos |o--o{ ideas : "scopes"
  ideas |o--o{ ideas : "parent of"
  tasks |o--o{ ideas : "converted from"

  workflow_templates |o--o{ workflows : "instantiated as"
  repos ||--o{ workflows : "runs"
  workflows |o--o{ tasks : "groups steps"

  tasks ||--o{ artifacts : "produces"
  tasks |o--o{ task_messages : "receives"

  repos ||--o{ agent_memory : "remembers"
  repos ||--o{ memory_facts : "knows"
  memory_facts ||--o{ memory_evidence : "supported by"
  agent_memory ||--o{ memory_evidence : "supported by"
  task_runs |o--o{ memory_evidence : "sourced from"
  repos ||--o{ corpus_documents : "indexes"

  mcp_servers ||--o{ repo_mcp_servers : "attached via"
  repos ||--o{ repo_mcp_servers : "enables"
  repos ||--o{ webhook_triggers : "accepts"
  task_templates |o--o{ webhook_triggers : "instantiates"
```

## Groups

| Group | Entities | Key point |
|---|---|---|
| Work | repos, tasks, task_runs, task_events, review_findings | Runs separate from tasks: retries, failover and cost stay queryable |
| Reuse | skill_sources, skills, skill_invocations, task_templates, schedules, schedule_runs | Each schedule fire keeps its own result folder |
| Planning | ideas, workflows, workflow_templates | Ideas form a tree. Conversion keeps the link. |
| Outputs | artifacts, task_messages | A message to a not-yet-created task key waits for it |
| Knowledge | agent_memory, memory_facts, memory_evidence, corpus_documents | Every memory traces to its source run. Lexical lane works without embeddings. |
| Integrations | mcp_servers, repo_mcp_servers, webhook_triggers | Tools enabled per repository |

Repo-less tasks exist for research and skills. A task can chain to a post-success script task.

## Not drawn

- **Queue tables.** Keyed by task id, no foreign keys. Queue retention never cascades into domain data.
- **Repository locks.** Keyed by repo name, with expiry. Admission, not a relationship.
- **Vault secrets and audit.** Addressed by scope and name. A secret outlives the repo that used it.
- **Settings, daily stats, workers, client tokens.**

## Modelling choices

- **CHECK constraints, not enums.** Enum values cannot be added inside a transaction.
- **Delete behaviour per edge.** Sent messages survive. Messages to a deleted task go with it, so a reused key never gets stale mail.
- **One transactional boundary.** Create task + enqueue = one commit.

Related: [Architecture](architecture.md) · [Reliability](reliability.md) · [Memory](../features/memory-and-knowledge.md) · [Skills and artifacts](../features/skills-and-artifacts.md) · [Ideas backlog](../features/ideas-backlog.md) · [Documentation](https://capitaltools.app/devagentforce/docs#backup)
