# Integrations — connecting an external tracker

**Pro.** **Connectors** (Settings → Connectors) import tracker items as **pending tasks or Ideas/Backlog entries — and stop there**. Nothing runs. Shipped: Azure DevOps.

## Set up

When the operator pastes a URL, say what goes where (the form does too, on blur):

| URL | Organization URL | Project |
|---|---|---|
| `https://dev.azure.com/<org>/<project>/_workitems/…` | `https://dev.azure.com/<org>` | `<project>` |
| `https://<org>.visualstudio.com/<project>/…` | the host | first path segment |
| `https://<host>/tfs/<collection>/<project>/_boards` (Server) | through the collection | `<project>` |

1. **+ Azure DevOps**. *Name* = audit tag `azure_devops:<name>`. No rename.
2. **PAT**: avatar → *User settings* → *Personal access tokens* → *New Token*. The URL's **organization**, an expiry, *Custom defined* scopes **Work Items → Read** + **Project and Team → Read**. Shown once. Paste in the form, **never in chat**.
3. **Assigned to** — name, e-mail or `@me`. Per import.
4. **Import into** — *Tasks (pending)* (repo, optional template) or *Ideas/Backlog* folder (its repo binding applies).
5. **Query** — WIQL; default = open items. `{{assignee}}` places the filter yourself.
6. **Save & Check connection** — account, project, PAT user, match count. Refusals show the tracker's message.

**Preview** (dry run) → **Import**. Re-imports skip unchanged, refresh pending, only *note* changes on started tasks. **Runs** = history.

## Failures

- **401 / "TF400813"** — wrong, expired or other-org PAT.
- **404 on Check** — project must match the URL exactly, spaces included.
- **0 matched** — assignee spelling or WIQL. Try `@me` + default query.
- **Page 404** — needs an active licence or trial.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#pro)
