---
id: p2-payment-gateway-when-legal-entity
type: backlog
project: aksara-karir
status: blocked
priority: p2
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, payments]
---

# Backlog: Payment gateway integration (Midtrans / Xendit)

## TL;DR

Replace manual bank transfer + proof upload with a real payment gateway once Aksara has a PT/CV.

## Description

- Choose: Midtrans, Xendit, or DOKU. Compare on fees, B2B invoicing, e-wallet coverage (GoPay/OVO/Dana/ShopeePay).
- Implement order/checkout flow; map to existing `t_enrollments` and payment status.
- Webhook handling for asynchronous confirmation.
- Keep manual flow as fallback for invoiced B2B contracts.
- Reconciliation and refund flows.

## Acceptance Criteria

- [ ] Aksara has PT/CV and merchant account.
- [ ] One gateway live in staging end-to-end.
- [ ] Manual + gateway flows coexist and are admin-distinguishable.
- [ ] Refund procedure documented.

## Priority

- Priority: p2 (blocked by client incorporation)

## Dependencies

- Blocked by: Aksara forming legal entity.
- Related ADR: [[Projects/aksara-karir/decisions/adr-2026-04-26-payment-manual-bank-transfer]]

## Links

- [[Projects/aksara-karir/docs/features/feat-registration]]
