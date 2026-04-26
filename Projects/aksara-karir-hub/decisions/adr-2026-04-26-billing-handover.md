---
id: adr-2026-04-26-billing-handover
type: adr
project: aksara-karir
status: proposed
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/adr, project/aksara-karir, commercial, ops]
---

# ADR — Billing handover for infra accounts

## TL;DR

All infra (Vercel, VPS, Supabase, R2, Resend, domain) is billed to mg's personal credit card. Decide whether and how to transfer ownership or pass-through bill these to Aksara Karir.

## Context

- Client has no PT/CV legal entity — payment gateway and many B2B billing options are blocked.
- Personal CC dependency means: if mg withdraws, client's LMS dies; if mg's card declines, prod outage.
- Some providers (Vercel, Supabase) support team transfers; R2 + VPS + domain transferable but require client account creation.

## Options

### Option A — Status quo

- Keep accounts on mg, expense via Lumen Dev.
- Pros: zero client friction.
- Cons: continued personal risk, no SLA story credible without it.

### Option B — Pass-through billing (recommended near-term)

- Keep accounts on mg, but charge **infra at cost + 15% admin** monthly to client.
- Itemized statement; client sees true cost.
- Pros: removes subsidy without forcing them to set up vendor accounts.
- Cons: still requires personal CC.

### Option C — Transfer ownership

- Aksara creates Vercel/Supabase/Cloudflare accounts; we co-administer.
- Pros: no personal exposure long-term.
- Cons: client needs legal entity for some providers (Cloudflare for-business, Vercel team), and operational maturity to manage billing.

## Decision

Pending. Recommendation: **B now, C as Aksara incorporates.**

## Consequences

- Need monthly itemized statement template.
- Need MSA / billing addendum to existing engagement letter (or create one if none exists).

## Alternatives Considered

- Lumen as billing intermediary using a Lumen company card — same effect as B, requires Lumen to have a card with sufficient credit limit.

## Related ADRs

- [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-subscription-pricing-model]]

## References

- [[Projects/aksara-karir-hub/context/commercial]]
