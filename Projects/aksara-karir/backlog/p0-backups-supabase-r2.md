---
id: p0-backups-supabase-r2
type: backlog
project: aksara-karir
status: ready
priority: p0
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, ops, backups]
---

# Backlog: Enable backups for Supabase Postgres and R2

## TL;DR

There are no backups today. A single corruption, accidental drop, or compromised admin account can destroy the entire learning history (enrollments, payments, certificate IDs, materials).

## Description

- Supabase: enable PITR (point-in-time recovery) on the prod project. Document retention period and restore procedure.
- R2: enable bucket versioning. Configure lifecycle rules to expire non-current versions after N days.
- Offsite: weekly DB dump (`pg_dump`) and R2 manifest copy to a different provider (e.g. Backblaze B2 or local NAS) — protects against full Cloudflare/Supabase account compromise.
- Document restore procedure in a runbook.

## Acceptance Criteria

- [ ] Supabase PITR enabled in dashboard. Tier upgrade noted in [[Projects/aksara-karir/context/commercial]] if needed.
- [ ] R2 bucket versioning enabled.
- [ ] Weekly offsite dump scripted and scheduled.
- [ ] Runbook `runbook-restore.md` written and tested with a non-prod restore.
- [ ] First successful test restore documented.

## Priority

- Priority: p0
- Rationale: no recovery path today; existential risk.

## Dependencies

- Blocked by: nothing.
- Related: [[Projects/aksara-karir/decisions/adr-2026-04-26-billing-handover]] (PITR may bump cost).

## Links

- N/A
