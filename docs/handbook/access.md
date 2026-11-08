# Signing in — the dashboard login

One operator, one password, every page guarded. Installers turn it **on**; native installs open a one-time `/welcome` link (24 h) to choose it — `devagentforce setup-link` makes a new one.

## Turn it on

1. `ENABLE_LOGIN_PAGE=true` (Settings `.env` editor or environment). Only `1`/`true` enable, only `0`/`false` disable — anything else **enables**. Read straight from `.env*`; works under bare `npm run dev`; applies in ~30 s.
2. `LOGIN_NAME` and `LOGIN_PASSWORD` — **both** must resolve, or the screen says nobody can sign in.

Then `/login` guards every page; unauthenticated `/api/*` gets `401`.

## Where the password lives

`process environment > .env file > secrets store`. Best: **Secrets** → `global/LOGIN_NAME`, `global/LOGIN_PASSWORD`, then delete them from `.env`. Host, out of history: `devagentforce-admin vault set global/LOGIN_PASSWORD --stdin`. ~30 s, no restart.

## Sessions

- Bound to the client address — a stolen cookie fails elsewhere, and the login screen says why. Proxy on **another** machine: `TRUST_PROXY_HEADERS=true` (reads `x-forwarded-for`).
- **Logout** in the header by the theme toggle. 12-hour sessions.
- No session table: **changing `LOGIN_PASSWORD` or `LOGIN_NAME` signs everyone out.** That is the revoke button.

## Open on purpose

Machine lanes — own credential or irreplaceable callback, no address binding:
`/api/auth/*` (login) · `/api/pro/a2a*` (bearer per peer) · `/api/pro/webhooks/*` (HMAC per trigger) · `/api/tasks/{id}/enqueue` (worker→web callback; closing it stops all tasks) · `/api/worker`, `/api/queue` (peer fleet control) · `/api/version`, `/.well-known/*`.

Your scripts: `INTERNAL_API_TOKEN` as `X-Internal-Token` on API paths.

## Locked out

On the dashboard host: set both keys, or `ENABLE_LOGIN_PAGE=false` — and check **every** `.env*` file, since any enabling line wins. No reset email, no second account.

It does not guard the **worker**: `/internal/*` has no auth — keep it on localhost or a private network. Other machines use Agent Peers (Pro) or webhook triggers.

---

[← Handbook index](README.md) · [Full documentation on capitaltools.app](https://capitaltools.app/devagentforce/docs#security)
