---
id: adr-2026-04-26-waha-vs-meta-cloud-api
type: adr
project: aksara-karir
status: accepted
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/adr, project/aksara-karir, whatsapp, ops]
---

# ADR — WAHA over Meta Cloud API for WhatsApp

## TL;DR

Use WAHA (unofficial WhatsApp HTTP API) self-hosted on a VPS for outbound notifications and admin messaging. Meta Cloud API is too expensive at MVP volume.

## Context

- Required: 1-hour-before class WhatsApp reminder, admin manual messages, OTP-style notifications.
- Volume: small (few hundred messages / month at MVP).
- Meta Cloud API: requires Business verification, template approval, per-message fees that don't suit current volume / cash flow.

## Decision

Run WAHA in Docker on a personal VPS. Use one WhatsApp number for outbound. Rotate or upgrade to Meta Cloud API only if the number is banned or volume crosses a threshold making fees comparable.

## Consequences

- WhatsApp number ban risk is real and increases with frequency / templated-marketing-style messages.
- WAHA sessions drop silently — operational toil. See [[Projects/aksara-karir-hub/runbooks/runbook-waha-session-restart]].
- No template approval = ToS gray zone.
- Cheap and flexible.

## Alternatives Considered

- Meta Cloud API: rejected due to cost / overhead at MVP.
- Email-only fallback: insufficient for the WhatsApp-first audience.
- Twilio: priced in USD, expensive.

## Related ADRs

- [[Projects/aksara-karir-hub/decisions/adr-2026-04-26-billing-handover]]

## References

- [[Projects/aksara-karir-hub/runbooks/runbook-waha-session-restart]]
- Future-state backlog item to revisit if banned: TBD when triggered.
