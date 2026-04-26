---
id: adr-2026-04-26-rls-vs-typeorm-only
type: adr
project: aksara-karir
status: proposed
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/adr, project/aksara-karir, security, supabase]
---

# ADR — RLS vs TypeORM-only access

## TL;DR

Decide whether to enable Supabase Row Level Security (RLS) and let clients hit PostgREST, or revoke `anon`/`authenticated` grants on all `public` tables and standardize on Next.js API routes using TypeORM with the service-role connection.

## Context

- The codebase already does all data access via Next.js API routes + TypeORM. `supabase-js` is used only for Auth.
- Local-dev SQL (in `AGENTS.md` and `scripts/`) explicitly grants `SELECT, INSERT, UPDATE, DELETE` on all `public` tables to `anon` and `authenticated`.
- It is currently unknown whether the same grants exist on the **production** Supabase project. If they do, the entire DB is publicly readable via the anon key (which is shipped to the browser by design).
- RLS is **not enabled**.

## Options

### Option A — TypeORM-only (recommended)

- Revoke all grants on `public` tables for `anon` and `authenticated`.
- Keep RLS off (or enable + leave deny-by-default; same effect with grants revoked).
- All reads/writes go through Next.js API routes using TypeORM with the service-role / Postgres connection string.
- Pros: matches what the code already does, single security surface, no per-table policy maintenance, simpler mental model.
- Cons: cannot use Supabase realtime subscriptions client-side; cannot use `supabase-js` for direct queries.

### Option B — RLS-first

- Enable RLS on every table; write per-role policies.
- Move some reads to client-side `supabase-js`.
- Pros: enables realtime, defense in depth, fewer round-trips for some screens.
- Cons: non-trivial policy engineering, every new table needs a policy or breaks the app, current code does not need it.

## Decision

Pending. Recommendation is Option A.

## Consequences

- If Option A: write a one-time SQL migration to revoke grants; rotate service-role key if leaked anywhere; document the model in `docs/architecture/`.
- If Option B: schedule a focused RLS-policy sprint, write tests, plan for breaking changes.

## Alternatives Considered

- Hybrid: enable RLS but keep API routes — adds maintenance burden without benefits while no client-side `supabase-js` queries exist.

## Related ADRs

- [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-billing-handover]]

## References

- Audit query: see [[Projects/aksara-karir-hub/runbooks/runbook-supabase-anon-grants-audit]]
- Backlog: [[Projects/aksara-karir-hub/backlog/p0-rls-or-revoke-anon]]
