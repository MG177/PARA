---
type: changelog
project: aksara-karir
status: done
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/changelog, project/aksara-karir]
---

# 2026-04-26 — Onboarding knowledge capture

## TL;DR

First structured capture of Aksara Karir project knowledge into the vault, beyond the in-repo `docs/` submodule. Establishes onboarding brief, client profile, system overview, commercial plan, ADRs for top open decisions, runbooks for top operational toil, and prioritized backlog.

## Change

- Rewrote [[Projects/aksara-karir/MOC]] to full governance template (TL;DR, Outcome, Status, Quick Links, Open Decisions, Active Backlog, Recent Changes, Risks & Blockers, Next Actions).
- Added project context notes (`context/`): onboarding-brief, client-profile, system-overview, commercial.
- Added ADRs: rls-vs-typeorm-only (proposed), subscription-pricing-model (proposed), billing-handover (proposed), payment-manual-bank-transfer (accepted), waha-vs-meta-cloud-api (accepted).
- Added runbooks: waha-session-restart, deploy, supabase-anon-grants-audit.
- Added 14 backlog items grouped p0–p3.
- Removed empty `Untitled.md` placeholder at project root.

## Reason

Project was delivered as one-time work without operational knowledge capture. We are preparing to pitch a paid retainer; need a single source of truth for client/system/commercial context, prioritized red flags, and decisions awaiting client input.

## Impact

- New developer or operator can onboard from `MOC.md` alone.
- Stabilization sprint scope is now defined (p0 + p1 backlog).
- Subscription proposal can reference concrete artifacts.

## Links

- [[Projects/aksara-karir/MOC]]
- [[Projects/aksara-karir/context/onboarding-brief]]
- [[Projects/aksara-karir/context/commercial]]
- [[Projects/aksara-karir/decisions/index]]
- [[Projects/aksara-karir/backlog/index]]
- [[Projects/aksara-karir/runbooks/index]]
