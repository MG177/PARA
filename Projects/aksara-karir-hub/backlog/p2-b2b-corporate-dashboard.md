---
id: p2-b2b-corporate-dashboard
type: backlog
project: aksara-karir
status: ready
priority: p2
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, b2b, enterprise]
---

# Backlog: B2B corporate dashboard

## TL;DR

PRD post-MVP roadmap. Stub UI exists at `src/app/enterprise/`. Build the real flow when client signs B2B clients (HR-managed cohorts, company billing, progress reports).

## Description

- Companies (`t_companies`) with HR admin users.
- Bulk enrollment of employees into courses / batches.
- Per-company dashboard: progress, attendance, certificates earned, quiz grades (when quizzes exist).
- Per-company invoicing flow (still likely manual until payment gateway).
- Reuse existing learner experience; HR is just a privileged scope.

## Acceptance Criteria

- [ ] Schema for `t_companies`, company-user membership, company-enrollment relationship.
- [ ] HR can see employee progress on a single dashboard.
- [ ] Unhide `src/app/enterprise/` after first paying B2B client.
- [ ] Documented pricing distinct from B2C in [[Projects/aksara-karir-hub/context/commercial]].

## Priority

- Priority: p2
- Rationale: revenue lever, but Aksara is not actively closing B2B yet.

## Dependencies

- Related: [[Projects/aksara-karir-hub/backlog/p1-admin-multi-account-audit]]
- Related: [[Projects/aksara-karir-hub/backlog/p2-payment-gateway-when-legal-entity]]

## Links

- [[Projects/aksara-karir/features/feat-prd-summary]]
