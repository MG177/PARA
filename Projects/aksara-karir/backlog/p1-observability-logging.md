---
id: p1-observability-logging
type: backlog
project: aksara-karir
status: ready
priority: p1
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, ops, observability]
---

# Backlog: Observability — error tracking, structured logging, uptime monitoring

## TL;DR

Currently there is no monitoring; outages are discovered when the client WhatsApps mg. Required for any credible SLA.

## Description

- **Error tracking**: Sentry (Next.js SDK) for client + server runtime errors. Free tier sufficient at MVP volume.
- **Structured logging**: replace `console.log` calls in API routes with a logger (pino or built-in `console` with structured JSON) that Vercel can index.
- **Uptime monitoring**: Better Stack / UptimeRobot pinging homepage + `/api/admin/waha/health` + key admin endpoint. Alert via WhatsApp + email.
- **Cron health**: Sentry cron monitors or dead-man-switch on each scheduled job — see [[Projects/aksara-karir/backlog/p0-cron-reminders-fix]].

## Acceptance Criteria

- [ ] Sentry receiving server + client events from prod.
- [ ] Uptime monitor configured for at least 3 endpoints.
- [ ] Alert delivered to mg's WA when a synthetic 5xx is triggered.
- [ ] Cron monitors green for 7 consecutive days.
- [ ] In `context/system-overview` updated with monitoring section.

## Priority

- Priority: p1
- Rationale: prerequisite for SLA, but not actively breaking users today.

## Dependencies

- Related: [[Projects/aksara-karir/backlog/p0-cron-reminders-fix]]

## Links

- [[Projects/aksara-karir/context/system-overview]]
