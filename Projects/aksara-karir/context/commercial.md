---
type: documentation
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/documentation, project/aksara-karir, commercial]
---

# Commercial — Subscription Pitch & Pricing

## TL;DR

Aksara Karir is currently on a one-time delivery contract with no SLA. The plan is to convert them to a paid retainer that funds operational ownership (backups, monitoring, security, WAHA babysitting) and unlocks future feature work (B2B, Zoom-API attendance, voucher logic). Key constraint: client is cash-strapped — pricing must respect that without subsidizing infra long-term.

## Engagement today

- One-time project, no SLA, comms via WhatsApp.
- All infra billed on **mg's personal credit card** — unsustainable as Aksara grows.
- Owner: mg (sole prod-access). Co-dev fallback: friend.

## Pricing options considered

### Option 1 — Tiered retainer (recommended)

| Tier | Price (IDR/mo) | Includes |
| --- | --- | --- |
| Lite | 500k | Uptime monitoring, weekly backup verification, security patches, 1 bug fix/mo, 24h response on WA business hours |
| Standard | 1.5jt | Lite + cron health checks + WAHA babysitting + 4hr response + 5 small content/config changes/mo |
| Growth | 3.5jt | Standard + 1 minor feature/mo + staging env + DKIM email + on-call weekends |

- Floor: 500k/mo.
- Add-on: **annual infra pass-through** (Vercel + VPS + Supabase + R2 + Resend at cost + 15% admin fee) so the personal CC stops absorbing growth.
- Add-on (one-time): **Stabilization fee** 3–5jt covering the 10 red flags in [[Projects/aksara-karir/context/onboarding-brief]]; paid upfront before retainer kicks in.

### Option 2 — Revenue share

- 0 base + **8–12% of paid enrollments** processed through the LMS, with a 750k/mo floor.
- Aligned incentives, but enforcement requires trust on enrollment counts (we already have read access).
- Risk: client could route enrollments outside the LMS to dodge the share.

### Option 3 — Per-active-student-month

- 5k IDR per active enrolled student/month, min 100k.
- Cleanest accounting; pushes client toward unit-economics thinking.
- Risk: client unfamiliar with SaaS billing models.

## Proposal structure (recommendation)

1. **Stabilization sprint (one-time fee)** — fix top 10 red flags before any retainer starts. Output: documented in [[Projects/aksara-karir/runbooks/index]] + ADRs.
2. **Tier 1 retainer (recurring)** — Aksara starts on Lite, upsells naturally as student volume grows.
3. **Infra pass-through (recurring)** — itemized monthly statement.
4. **New features quoted separately** — explicit exclusion list (B2B build, design overhauls, data migrations, payment gateway integration when legal entity ready).

## Exclusion list (must be in the contract)

- New features and major design changes.
- Data migrations and schema redesigns.
- Payment gateway integration (depends on Aksara legal entity).
- WhatsApp Cloud API migration if WAHA becomes untenable.
- Legal/compliance work (data residency audits, ToS, privacy policy reviews).

## Open commercial decisions

- See [[Projects/aksara-karir/decisions/adr-2026-04-26-subscription-pricing-model]]
- See [[Projects/aksara-karir/decisions/adr-2026-04-26-billing-handover]]

## Pitch artifacts to produce

- [ ] Indonesian-language proposal PDF.
- [ ] English-language summary (1-pager).
- [ ] Itemized infra cost statement template (monthly).
- [ ] Stabilization sprint scope doc (links to all p0/p1 backlog items).
