---
id: p3-discount-voucher-logic
type: backlog
project: aksara-karir
status: draft
priority: p3
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, payments]
---

# Backlog: Discount and voucher logic

## TL;DR

No discount or voucher engine exists today. Add later when marketing campaigns require it.

## Description

- Voucher codes: percent, fixed amount, single-use vs multi-use, per-course vs global.
- Bulk codes generation for campaigns.
- Admin UI to manage codes.
- Reporting on redemption.

## Acceptance Criteria

- [ ] `t_vouchers` table.
- [ ] Apply / validate at registration time.
- [ ] Audit redemptions per code.

## Priority

- Priority: p3
- Rationale: not currently requested by client.

## Dependencies

- None.

## Links

- [[Projects/aksara-karir/docs/features/feat-registration]]
