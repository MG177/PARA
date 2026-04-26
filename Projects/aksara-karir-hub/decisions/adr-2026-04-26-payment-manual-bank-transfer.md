---
id: adr-2026-04-26-payment-manual-bank-transfer
type: adr
project: aksara-karir
status: accepted
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/adr, project/aksara-karir, payments]
---

# ADR — Manual bank transfer + admin proof verification

## TL;DR

The LMS does not integrate any payment gateway. Users pay by manual bank transfer and upload a proof image; admins verify and unlock enrollment.

## Context

- Aksara Karir lacks a legal entity (PT/CV) — Indonesian payment gateways (Midtrans, Xendit, etc.) require this for merchant onboarding.
- Volume is low at MVP, so manual ops is tolerable.

## Decision

Manual bank transfer flow:

1. User submits registration form including target course + bank transfer details acknowledgement.
2. User uploads proof image; stored in R2.
3. Admin sees pending payments at `/admin/payment-proof`, verifies, marks paid; enrollment activates.

## Consequences

- No automated reconciliation — admin error possible.
- No partial payments or installments.
- No automated refunds.
- Admin throughput is the cap on enrollment volume.
- Migration to a gateway is a future feature gated on Aksara incorporating.

## Alternatives Considered

- Stripe / international: blocked by IDR + tax + entity constraints.
- E-wallet (GoPay, OVO) personal accounts: messy for B2B receipts.

## Related ADRs

- [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-billing-handover]]

## References

- [[Projects/aksara-karir/features/feat-registration]]
- Backlog: [[Projects/aksara-karir-hub/backlog/p2-payment-gateway-when-legal-entity]]
