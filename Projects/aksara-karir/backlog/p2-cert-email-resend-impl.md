---
id: p2-cert-email-resend-impl
type: backlog
project: aksara-karir
status: ready
priority: p2
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, certificates, email]
---

# Backlog: Implement certificate email delivery (Resend)

## TL;DR

PRD and vault docs both say certificates are emailed on issuance. Resend env vars are wired, but the send path is not implemented. Implement it.

## Description

- On admin marking completion → cert PDF is generated → email user with PDF attached or link to download.
- Use Resend; verify sender domain (DKIM/SPF) — likely needs domain on Aksara's DNS, not mg's.
- Include verify link with QR pointing at `/api/public/certificates/pdf?id=...`.
- Make graceful: if `RESEND_API_KEY` missing, skip silently with a log, do not block completion.

## Acceptance Criteria

- [ ] Sender domain verified with DKIM + SPF.
- [ ] Email template (HTML + text) exists.
- [ ] Test certificate emailed and received in inbox (not spam) on Gmail and one corporate provider.
- [ ] Failure path logged; does not crash completion mark.

## Priority

- Priority: p2
- Rationale: PRD-listed, low-effort, client-visible polish.

## Dependencies

- Related: [[Projects/aksara-karir/backlog/p2-cert-template-flexibility]]
- Related: [[Projects/aksara-karir/backlog/p1-observability-logging]] (delivery telemetry)

## Links

- [[Projects/aksara-karir/docs/features/feat-certificates]]
