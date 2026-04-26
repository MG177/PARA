---
id: p1-r2-garbage-collection
type: backlog
project: aksara-karir
status: ready
priority: p1
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, r2, ops]
---

# Backlog: R2 garbage collection / orphan sweeper

## TL;DR

Files uploaded to R2 are never automatically deleted. Bill grows linearly forever. Today mg deletes manually. Need a scheduled sweeper for orphans (DB record gone) and expired (`expiration_date` past) materials.

## Description

- Define orphan = R2 object whose key is not referenced by any `t_files` row.
- Define expired = `t_files` row with `expiration_date < now()` past a grace window (e.g. 7 days).
- Daily job (separate from cleanup-expired or extending it) that:
  1. Lists R2 objects with pagination.
  2. Diffs against DB.
  3. Reports orphans first (dry run for at least 1 week), then enables actual deletion.
- Track storage size over time so client can be billed pass-through accurately.

## Acceptance Criteria

- [ ] Sweeper script exists under `scripts/` and as cron route under `/api/cron/files/`.
- [ ] Dry-run output stored / logged for review for ≥7 days.
- [ ] Live deletion gated behind env flag and ADR / changelog entry.
- [ ] Storage size metric exposed in admin dashboard or logged daily.

## Priority

- Priority: p1
- Rationale: cost grows without bound; not user-facing yet.

## Dependencies

- Related: [[Projects/aksara-karir/backlog/p0-cron-reminders-fix]] (same scheduler infra)

## Links

- [[Projects/aksara-karir/docs/features/feat-file-repository]]
- [[Projects/aksara-karir/docs/data-model/db-schema-t-files]]
