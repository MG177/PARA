---
id: p0-rls-or-revoke-anon
type: backlog
project: aksara-karir
status: ready
priority: p0
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, security, supabase]
---

# Backlog: Audit and lock down anon/authenticated grants on prod DB

## TL;DR

Confirm whether the prod Supabase Postgres has over-broad grants on `public` tables for `anon`/`authenticated`. If yes, revoke. Standardize on TypeORM-only access through Next.js API routes.

## Description

- Local-dev SQL grants `SELECT, INSERT, UPDATE, DELETE` on all `public` tables to `anon` and `authenticated`.
- RLS is not enabled.
- If those grants exist on prod, the anon key (which is shipped to browsers) can read all user, enrollment, and payment data via PostgREST.
- The codebase already uses TypeORM with the service-role connection; revoking grants does not affect normal app operation.

## Acceptance Criteria

- [ ] Audit query run; results saved under `runbooks/audit-results/` (or attached to ADR).
- [ ] If grants exist on user/payment tables: revocation SQL applied.
- [ ] Smoke checks pass post-revocation: register, login, admin list, file streaming, certificate download.
- [ ] [[Projects/aksara-karir/decisions/adr-2026-04-26-rls-vs-typeorm-only]] moved from `proposed` to `accepted`.
- [ ] In-repo `docs/architecture/` updated to document the access model.

## Priority

- Priority: p0
- Rationale: potential PII exposure; blocking issue for SLA story.

## Dependencies

- Blocked by: nothing.
- Related ADR: [[Projects/aksara-karir/decisions/adr-2026-04-26-rls-vs-typeorm-only]]
- Related runbook: [[Projects/aksara-karir/runbooks/runbook-supabase-anon-grants-audit]]

## Links

- Architecture: [[Projects/aksara-karir/docs/architecture/arch-overview]]
