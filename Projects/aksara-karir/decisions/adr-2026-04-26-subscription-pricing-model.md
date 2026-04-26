---
id: adr-2026-04-26-subscription-pricing-model
type: adr
project: aksara-karir
status: proposed
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/adr, project/aksara-karir, commercial]
---

# ADR — Subscription pricing model

## TL;DR

Choose how to charge Aksara Karir for ongoing operational ownership and feature work post-MVP.

## Context

- Project delivered as one-time. No retainer, no SLA.
- Client is cash-strapped (early-stage startup, no PT/CV).
- Lumen (mg) carries all infra costs on personal credit card.
- Initial price idea floated by mg: 250–500k IDR/mo. Likely below cost once infra grows.

## Options

### Option 1 — Tiered retainer (Lite 500k / Standard 1.5jt / Growth 3.5jt) + infra pass-through

- Floor protects margin; client starts low and grows.
- Infra pass-through ends personal-CC subsidy.
- Optional one-time stabilization fee 3–5jt.

### Option 2 — Revenue share (8–12% of paid enrollments, 750k floor)

- Aligned incentives; light cognitive load on client.
- Enforcement risk if client routes enrollments outside the LMS.

### Option 3 — Per-active-student-month (5k IDR/student, 100k floor)

- Cleanest SaaS-style billing.
- Unfamiliar to client; may slow signing.

## Decision

Pending. Recommendation: **Option 1** with mandatory infra pass-through and one-time stabilization fee.

## Consequences

- Need itemized monthly infra cost statement template.
- Need clear exclusion list in the contract (see [[Projects/aksara-karir/context/commercial]]).
- Pricing escalators per tier should be defined upfront.

## Alternatives Considered

- Free maintenance with paid features-only: rejected — does not cover ops cost or risk.
- Equity in lieu of cash: rejected — early stage, dilution risk for unclear return.

## Related ADRs

- [[Projects/aksara-karir/decisions/adr-2026-04-26-billing-handover]]

## References

- [[Projects/aksara-karir/context/commercial]]
