---
id: p3-zoom-attendance-api
type: backlog
project: aksara-karir
status: draft
priority: p3
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, zoom, attendance]
---

# Backlog: Zoom API attendance integration

## TL;DR

Today admin manually marks completion based on Aksara's external attendance system. Integrate Zoom API to pull attendance and auto-suggest completion.

## Description

- Zoom Server-to-Server OAuth app.
- Pull participant join/leave times after each meeting.
- Match by email / phone to enrolled users.
- Compute attendance percentage; auto-mark completion above threshold (admin can override).
- Listed in PRD post-MVP roadmap.

## Acceptance Criteria

- [ ] Zoom credentials in env; documented.
- [ ] Per-batch attendance report visible in admin.
- [ ] Auto-suggested completion for users above threshold.
- [ ] Manual override preserved.

## Priority

- Priority: p3
- Rationale: nice-to-have; current manual flow works.

## Dependencies

- None.

## Links

- [[Projects/aksara-karir/features/feat-prd-summary]]
- [[Projects/aksara-karir/features/feat-certificates]]
