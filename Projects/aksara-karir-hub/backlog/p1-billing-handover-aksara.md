---
id: p1-billing-handover-aksara
type: backlog
project: aksara-karir
status: ready
priority: p1
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, commercial, ops]
---

# Backlog: Billing handover plan for infra accounts

## TL;DR

All infra accounts are on mg's personal credit card. Implement pass-through billing now; transfer ownership when Aksara incorporates.

## Description

- Build itemized monthly statement template (Vercel + VPS + Supabase + R2 + Resend + domain).
- Add 15% admin fee line.
- Define escalation: when the client's monthly statement exceeds X IDR or they have a legal entity, trigger account transfer (Option C in [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-billing-handover]]).
- Document each provider's transfer procedure.

## Acceptance Criteria

- [ ] Statement template exists.
- [ ] First statement sent to client.
- [ ] Provider-by-provider transfer procedure documented.
- [ ] Trigger threshold agreed and recorded in ADR.

## Priority

- Priority: p1
- Rationale: removes single-person financial dependency; enables credible SLA.

## Dependencies

- Related ADR: [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-billing-handover]]
- Related: [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-subscription-pricing-model]]

## Links

- [[Projects/aksara-karir-hub/context/commercial]]
