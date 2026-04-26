---
type: moc
status: active
area: lumendev
project: aksara-karir
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [project, area/lumendev, aksara-karir, type/moc]
---

# Aksara Karir (LMS)

## TL;DR

LMS for **Aksara Karir** (online mining/geology training, Indonesia) delivered by Lumen Dev as a one-time project; MVP shipped, currently in unmaintained "done" state. Next milestone: **stabilization sprint + subscription proposal** so we can take over operational ownership before incidents grow.

## Outcome

- Problem: client ran courses via Zoom + WhatsApp + spreadsheets; needed a web LMS for registration, schedule, files, certificates.
- Desired outcome: stable platform we maintain under a paid retainer, with B2B and Zoom-API attendance as future upsells.
- Success metric: zero P0 incidents/month after stabilization, signed retainer ≥ 750k IDR/mo, billing handover off personal credit card.
- Scope (in): Next.js LMS app, Supabase, Cloudflare R2, WAHA, certificates.
- Scope (out): client's Zoom attendance system, marketing site, payment gateway (until client has legal entity).

## Status

- Current phase: post-MVP, awaiting stabilization sprint.
- Next milestone: prod security audit (anon grants) → red-flag triage → subscription pitch.
- Target date: 2026-05 (audit + pitch); stabilization through 2026-06.
- Health: yellow — works in prod but several latent risks (no backups, no monitoring, crons not running, single shared admin, single ops owner).

## Quick Links

- Project context (hub): [[Projects/aksara-karir/context/index]]
- Technical docs (in-repo submodule, source of truth): [[Projects/aksara-karir/docs/README]]
- Decisions: [[Projects/aksara-karir/decisions/index]]
- Backlog: [[Projects/aksara-karir/backlog/index]]
- Runbooks: [[Projects/aksara-karir/runbooks/index]]
- Changelog: [[Projects/aksara-karir/changelog/index]]
- Area: [[Areas/LumenDev]]

## Project folders (what goes where)

| Folder | Use for | Do not use for |
| --- | --- | --- |
| **`context/`** | Client, commercial, onboarding, handover, short vault-side system summary; hub **`context/index.md`**. | Technical specs duplicated from the repo — link to **`docs/README`** instead. |
| **`docs/`** | Technical / product docs with the codebase (architecture, data model, APIs, tests). Hub **`docs/README.md`**. | Client notes, ADRs, backlog — use `context/`, `decisions/`, `backlog/`. |
| **`decisions/`** | ADRs and dated “we chose X” records. | Operator procedures or task lists. |
| **`runbooks/`** | Repeatable ops procedures. | Product requirements or ADR rationale. |
| **`backlog/`** | Prioritized work and owners. | Long-form reference docs. |
| **`meetings/`** | Meeting-specific notes. | Evergreen architecture writeups. |
| **`changelog/`** | Dated narrative of what changed in the vault or project story. | Git history by default. |
| **`archive/`** | Superseded notes. | Active work. |

**One-line test:** if every open task and meeting disappeared, would this note still help someone understand the project? If yes → **`context/`** or **`docs/`** (technical); choice records → **`decisions/`**; “when X happens, do Y” → **`runbooks/`**.

## Open Decisions

- [ ] [[Projects/aksara-karir/decisions/adr-2026-04-26-rls-vs-typeorm-only]] — RLS or revoke anon and standardize on TypeORM-only access?
- [ ] [[Projects/aksara-karir/decisions/adr-2026-04-26-subscription-pricing-model]] — Tiered retainer vs revenue share vs per-student.
- [ ] [[Projects/aksara-karir/decisions/adr-2026-04-26-billing-handover]] — Move infra accounts off personal credit card?

## Active Backlog

- [ ] [[Projects/aksara-karir/backlog/p0-rls-or-revoke-anon]] — p0 — mg
- [ ] [[Projects/aksara-karir/backlog/p0-cron-reminders-fix]] — p0 — mg
- [ ] [[Projects/aksara-karir/backlog/p0-backups-supabase-r2]] — p0 — mg
- [ ] [[Projects/aksara-karir/backlog/p1-observability-logging]] — p1 — mg
- [ ] [[Projects/aksara-karir/backlog/p1-r2-garbage-collection]] — p1 — mg
- [ ] [[Projects/aksara-karir/backlog/p1-admin-multi-account-audit]] — p1 — mg
- [ ] [[Projects/aksara-karir/backlog/p1-staging-environment]] — p1 — mg
- [ ] [[Projects/aksara-karir/backlog/p1-billing-handover-aksara]] — p1 — mg
- [ ] [[Projects/aksara-karir/backlog/p2-cert-email-resend-impl]] — p2 — mg
- [ ] [[Projects/aksara-karir/backlog/p2-cert-template-flexibility]] — p2 — mg
- [ ] [[Projects/aksara-karir/backlog/p2-b2b-corporate-dashboard]] — p2 — mg
- [ ] [[Projects/aksara-karir/backlog/p2-payment-gateway-when-legal-entity]] — p2 — mg
- [ ] [[Projects/aksara-karir/backlog/p3-discount-voucher-logic]] — p3 — mg
- [ ] [[Projects/aksara-karir/backlog/p3-zoom-attendance-api]] — p3 — mg

## Recent Changes

- 2026-04-26 — [[Projects/aksara-karir/changelog/2026-04-26-onboarding-knowledge-capture]] — captured client, stack, ops, and risk knowledge into vault.

## Risks & Blockers

- Risk: WAHA session drops silently (unofficial WhatsApp) | Impact: scheduled reminders fail, possible WA number ban | Mitigation: see [[Projects/aksara-karir/runbooks/runbook-waha-session-restart]]; long-term migrate to Meta Cloud API or add email fallback | Owner: mg
- Risk: anon role may have over-broad grants on prod (no RLS) | Impact: PII / payment proof URLs publicly readable | Mitigation: run grants audit, revoke or apply RLS — see [[Projects/aksara-karir/decisions/adr-2026-04-26-rls-vs-typeorm-only]] | Owner: mg
- Risk: no backups (Supabase + R2) | Impact: total data loss on corruption / accidental drop | Mitigation: enable Supabase PITR, R2 lifecycle + offsite copy | Owner: mg
- Risk: all infra billed on personal credit card | Impact: dependency on individual; client cannot operate if Lumen withdraws | Mitigation: billing handover plan, see [[Projects/aksara-karir/decisions/adr-2026-04-26-billing-handover]] | Owner: mg
- Risk: cron reminders not scheduled in Vercel | Impact: 1-hour-before WhatsApp class reminder silently disabled | Mitigation: schedule via Vercel Cron or Supabase scheduled function | Owner: mg
- Risk: single shared admin login | Impact: no audit trail, no per-user revoke | Mitigation: per-admin Supabase users + role table | Owner: mg
- Risk: bus factor of one (mg) for prod access | Impact: outage risk if owner unavailable | Mitigation: shared 1Password vault with co-dev (friend), documented runbooks | Owner: mg

## Next Actions

- [ ] Run anon-grants audit on prod Supabase — mg — due 2026-05-03
- [ ] Schedule cron reminders + cleanup-expired in Vercel — mg — due 2026-05-03
- [ ] Enable Supabase PITR + R2 versioning/lifecycle — mg — due 2026-05-10
- [ ] Draft subscription proposal (Indonesian + English) — mg — due 2026-05-10
- [ ] Send proposal + stabilization quote to Aksara Karir — mg — due 2026-05-17

## Related

- [[Areas/LumenDev]]
- App repo (local): `~/Project/aksara-karir-lms`
- Technical docs (`docs/` submodule): [[Projects/aksara-karir/docs/README]] — https://github.com/MG177/aksara-karir-lms-docs
- Initial PRD (Notion): https://www.notion.so/2e8bdcdd44cd80a496ebfa0f467cf493
