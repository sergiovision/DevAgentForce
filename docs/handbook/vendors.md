# Agents, models and billing

Pick a coding-agent CLI per task on the **Vendor | Model | Billing** row.

| Vendor | CLI | Notes |
|---|---|---|
| **Anthropic** | `claude` | Claude Code. Most exercised |
| **Google** | `agy` | Antigravity. Effort in the name: `gemini-3.1-pro-high`, `gemini-4-argon-high` (Gemini 4 Argon) |
| **OpenAI** | `codex` | |
| **Pi** | `pi` | Any OpenAI-compatible endpoint (OpenRouter, Z.AI). Off by default |

- New vendor → its default model.
- `claude-opus-latest`, `gemini-argon-latest`, `gpt-latest` float to the newest; Settings shows the mapping.
- CLI missing on the worker → instant *"CLI not found"*.
- **Active** off (Settings → Vendors): hidden from Sessions and pickers; new tasks refused, queued fail, running finish. Saved records keep the value.

## Pi

**Settings → Vendors**: on → install (Node 22.19+) → endpoint (OpenRouter, Z.AI, Z.AI Coding Plan — that key needs its own preset) → **Test** (proves tool calls). Models show as `provider/model`. Always API billing; never System LLM.
- **OS sandbox** macOS/Linux (`pi_sandbox`: Off, Auto, Required): writes only task folders, no credentials, network open. Otherwise, and on Windows: untrusted repos on a disposable VM.
- Price paid models so a dollar budget (Pro) applies.
- **Pi packages** — pinned `npm:`/`git:`. **Install**, enable. They run in Pi and can read the endpoint key.

## Billing

- **Max (subscription)** — API key stripped; host OAuth login (Claude Max, ChatGPT Plus, Google AI Pro). Flat fee. Usual choice. Cost charts read `$0`.
- **API Platform** — CLI uses your key, per-token. Needed for cost tracking.

## Failover and rate limits

- **Backup vendor + model**: after the primary's retries (incl. rate-limit backoff), a fresh loop — new session, committed work kept, errors cleared. Unset vendor = same-vendor downgrade (Opus → Sonnet); different vendor = cross-vendor.
- **429**: retried in-call at 30 s, 60 s, 120 s + jitter, no attempt burned; `rate_limit_backoff` on the timeline. Cause: too many concurrent tasks per vendor.

**System LLM** (Settings) is separate: a cheaper model for Fill Task, DevPlan, compaction, this assistant. Own vendor, model, billing.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#vendors)
