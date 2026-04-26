---
type: documentation
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/documentation, project/aksara-karir, client]
---

# Client Profile — Aksara Karir

## TL;DR

Aksara Karir is an Indonesian online-learning startup focused on mining and geology training. Lumen Dev built and ships their LMS as a one-time engagement; relationship is informal and sole channel is WhatsApp.

## Business

- Industry: online education, niche **mining and geology**.
- Format: live Zoom courses, optional recordings, certificate of completion per course.
- Stage: **early-stage**, revenue inconsistent, **no legal entity (PT/CV) yet** — meaning no merchant account, no payment gateway integration possible currently.
- Audience: junior students and early-career professionals in mining/geology in Indonesia.

## Engagement with Lumen Dev

- Type: **one-time project** (not a retainer).
- Sign-off / veto: none formally. No SLA. No documented support expectation.
- Communication: **WhatsApp only**. No tickets, no email threads, no shared workspace.
- Owner on Lumen side: **mg** (sole). Co-dev (friend) as backup capacity, not yet onboarded operationally.
- Owner on Aksara side: small admin team using one shared account on the LMS.

## Constraints driven by client

- No payment gateway → manual bank transfer + admin proof verification.
- No formal QA / acceptance process → "client says it works" is the bar.
- Limited budget for ongoing fees → infrastructure pass-through pricing must be transparent.
- WhatsApp-first communication shapes all notifications (and is itself a fragile dependency, see WAHA).

## Future opportunities

- **Subscription / maintenance retainer** — see [[Projects/aksara-karir-hub/context/commercial]].
- **B2B corporate dashboard** — already drafted in PRD post-MVP roadmap, hidden stub at `src/app/enterprise/`.
- **Zoom-API attendance integration** — eliminates manual admin completion marking.
- **Pre/post test quizzes** — competency gating before certificate (also in PRD post-MVP roadmap).
