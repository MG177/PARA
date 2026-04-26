---
type: runbook
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/runbook, project/aksara-karir, security, supabase]
---

# Runbook — Supabase anon grants audit

## TL;DR

Verify whether the prod Supabase Postgres has over-broad grants on `public` tables for `anon` / `authenticated` (a side-effect of the local-dev SQL snippet in `AGENTS.md`). Required pre-step for [[Projects/aksara-karir/decisions/adr-2026-04-26-rls-vs-typeorm-only]].

## Scope

- Production Supabase project only.
- Does not modify data; read-only SQL.

## Preconditions

- `DATABASE_URL` for prod (from Supabase Dashboard → Project settings → Database → Connection string, session-mode pooler or direct).
- `psql` installed.

## Procedure

1. Connect:
   ```bash
   psql "$DATABASE_URL"
   ```
2. List grants:
   ```sql
   SELECT table_schema, table_name, grantee, privilege_type
   FROM information_schema.role_table_grants
   WHERE grantee IN ('anon', 'authenticated')
     AND table_schema = 'public'
   ORDER BY table_name, grantee, privilege_type;
   ```
3. Check RLS status:
   ```sql
   SELECT schemaname, tablename, rowsecurity
   FROM pg_tables
   WHERE schemaname = 'public'
   ORDER BY tablename;
   ```
4. Save output to `Projects/aksara-karir/runbooks/audit-results/<date>.md` (create folder if needed).

## Interpretation

- **Bad:** `anon` has any `SELECT/INSERT/UPDATE/DELETE` on `public.t_users`, `public.t_enrollments`, `public.t_payment_proofs`, etc., **and** `rowsecurity = false`. This means the anon key (shipped to browsers) can read user data.
- **Acceptable:** `anon` only has rights on intentionally public tables (e.g. `t_courses` listing) and nothing on user/payment data.
- **Best:** no grants to `anon`/`authenticated` on `public` at all (TypeORM-only model).

## Rollback

- N/A — read-only.

## If grants are too broad — remediation

```sql
REVOKE SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public FROM anon, authenticated;
ALTER DEFAULT PRIVILEGES IN SCHEMA public REVOKE SELECT, INSERT, UPDATE, DELETE ON TABLES FROM anon, authenticated;
NOTIFY pgrst, 'reload schema';
```

Then verify the app still works (TypeORM uses the service-role connection, so it should be unaffected).

## Validation

- Post-revoke: `\dp` shows no anon/authenticated rights on user/payment tables.
- App: registration, login, admin list, file streaming, certificate download all work.

## Related Incidents

- None confirmed yet — this audit determines if there is one.

## References

- [[Projects/aksara-karir/decisions/adr-2026-04-26-rls-vs-typeorm-only]]
- [[Projects/aksara-karir/backlog/p0-rls-or-revoke-anon]]
