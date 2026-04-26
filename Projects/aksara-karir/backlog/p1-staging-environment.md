---
id: p1-staging-environment
type: backlog
project: aksara-karir
status: ready
priority: p1
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, deploy]
---

# Backlog: Staging environment

## TL;DR

Every push lands in prod. Need a staging branch + Vercel preview env + a non-prod Supabase project so risky changes can be validated before customers see them.

## Description

- Create `staging` branch; configure Vercel to deploy `staging` to a stable preview URL.
- Provision a second Supabase project for staging; copy schema (`scripts/supabase-init.sql` + migrations) but seed with synthetic data.
- Provision a second R2 bucket for staging.
- Run a separate WAHA session (different number) for staging or stub WhatsApp sends in staging.
- Document promotion: staging → main as a PR + e2e gate.

## Acceptance Criteria

- [ ] Staging URL reachable, distinct from prod.
- [ ] `.env.staging` example documented (without secrets).
- [ ] e2e tests run against staging in CI (future) or locally with staging env.
- [ ] Promotion checklist in [[Projects/aksara-karir/runbooks/runbook-deploy]].

## Priority

- Priority: p1
- Rationale: risk reduction for ongoing maintenance.

## Dependencies

- Related: [[Projects/aksara-karir/backlog/p1-observability-logging]]

## Links

- [[Projects/aksara-karir/runbooks/runbook-deploy]]
