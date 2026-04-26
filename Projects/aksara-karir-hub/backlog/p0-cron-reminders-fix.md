---
id: p0-cron-reminders-fix
type: backlog
project: aksara-karir
status: ready
priority: p0
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, cron, whatsapp]
---

# Backlog: Schedule cron jobs in Vercel (reminders + R2 cleanup)

## TL;DR

Cron routes exist in code (`/api/cron/reminders/class`, `/api/cron/files/cleanup-expired`) but are not scheduled. The 1-hour-before WhatsApp class reminder — a delivered PRD feature — is silently disabled in prod.

## Description

- Add `crons` entries to `vercel.json` (or Vercel Dashboard schedules).
- Reminder cron: every 5 minutes; route is idempotent and uses a 55–65 minute lookahead window.
- Cleanup cron: daily; soft-deletes / marks expired R2 materials.
- Both routes already require `CRON_SECRET` header — verify Vercel Cron passes it correctly.
- If Vercel cron limits hurt (Hobby plan), evaluate Supabase scheduled functions or an external scheduler.

## Acceptance Criteria

- [ ] `vercel.json` contains both schedules and is deployed.
- [ ] Vercel Dashboard shows last execution success.
- [ ] Real test: schedule a class 70 minutes out → reminder arrives within the 55–65 min window.
- [ ] Cleanup cron runs at least once and logs the count of expired files acted on.
- [ ] Logged failures alert mg (depends on [[Projects/aksara-karir-hub/backlog/p1-observability-logging]]).

## Priority

- Priority: p0
- Rationale: paid feature is broken in production.

## Dependencies

- Blocks: nothing critical.
- Blocked by: nothing.
- Related: [[Projects/aksara-karir-hub/backlog/p1-observability-logging]]

## Links

- [[Projects/aksara-karir/features/feat-schedule]]
