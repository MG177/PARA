---
id: p1-admin-multi-account-audit
type: backlog
project: aksara-karir
status: ready
priority: p1
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, security, admin]
---

# Backlog: Per-admin accounts and audit log

## TL;DR

Today there is one shared admin login. No way to know who verified a payment or marked completion. No revoke-on-leave story. Add per-admin accounts with a role table and minimal audit log.

## Description

- Add a `role` column or `t_user_roles` table. Roles: `admin`, `instructor`, `student` (instructor route exists; confirm semantics).
- Each Aksara staff member gets a Supabase Auth user.
- Add `t_admin_actions` (or generalized audit) capturing: actor user_id, action, target_id, timestamp, ip.
- Hook on key admin actions: payment verification, completion mark, file upload, file deletion.
- Admin page to view recent actions per user.

## Acceptance Criteria

- [ ] Migration adds role + audit tables.
- [ ] At least 2 distinct admin accounts in use; shared account deactivated.
- [ ] Audit log records the targeted actions.
- [ ] Off-boarding procedure documented (deactivate user, force sign-out).

## Priority

- Priority: p1
- Rationale: needed for any compliance / SLA conversation; low user impact today.

## Dependencies

- Related: [[Projects/aksara-karir/backlog/p1-observability-logging]]

## Links

- [[Projects/aksara-karir/docs/features/feat-registration]]
