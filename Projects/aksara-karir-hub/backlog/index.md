---
type: index
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/index, project/aksara-karir, backlog]
---

# Backlog Index

## p0 — Stabilization (must do before any subscription pitch)

- [[Projects/aksara-karir-hub/backlog/p0-rls-or-revoke-anon]] — verify and lock down DB grants
- [[Projects/aksara-karir-hub/backlog/p0-cron-reminders-fix]] — schedule WA reminder + R2 cleanup crons in Vercel
- [[Projects/aksara-karir-hub/backlog/p0-backups-supabase-r2]] — enable Supabase PITR and R2 versioning + offsite copy

## p1 — Operational maturity

- [[Projects/aksara-karir-hub/backlog/p1-observability-logging]] — Sentry / structured logging / uptime monitoring
- [[Projects/aksara-karir-hub/backlog/p1-r2-garbage-collection]] — orphan + expired blob sweeper
- [[Projects/aksara-karir-hub/backlog/p1-admin-multi-account-audit]] — per-admin accounts, audit log, role table
- [[Projects/aksara-karir-hub/backlog/p1-staging-environment]] — Vercel preview / staging branch + DB
- [[Projects/aksara-karir-hub/backlog/p1-billing-handover-aksara]] — pass-through + transfer plan

## p2 — Client-requested features

- [[Projects/aksara-karir-hub/backlog/p2-cert-email-resend-impl]] — implement Resend-based certificate delivery
- [[Projects/aksara-karir-hub/backlog/p2-cert-template-flexibility]] — per-course / per-batch certificate templates
- [[Projects/aksara-karir-hub/backlog/p2-b2b-corporate-dashboard]] — unhide and build the enterprise stub
- [[Projects/aksara-karir-hub/backlog/p2-payment-gateway-when-legal-entity]] — Midtrans / Xendit when Aksara has PT/CV

## p3 — Nice to have

- [[Projects/aksara-karir-hub/backlog/p3-discount-voucher-logic]] — voucher / discount engine
- [[Projects/aksara-karir-hub/backlog/p3-zoom-attendance-api]] — auto-completion via Zoom API
