---
type: documentation
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/documentation, project/aksara-karir, architecture]
---

# System Overview (vault-side summary)

## TL;DR

High-signal pointer doc. Canonical architecture and data-model docs live in the in-repo submodule under [[Projects/aksara-karir/docs/README]]. This file captures only the operational realities and gaps the in-repo docs currently omit.

## At-a-glance stack

| Layer | Choice |
| --- | --- |
| Framework | Next.js 16 App Router, React 19, TypeScript |
| Hosting | Vercel (auto-deploy from `main`, no staging, no preview env in use) |
| Auth | Supabase Auth — email + password only |
| DB | Supabase Postgres — accessed via TypeORM (service role) from API routes; RLS not enabled |
| File storage | Cloudflare R2 via `@aws-sdk/*` (presigned URL + multipart upload) |
| WhatsApp | WAHA (unofficial) in Docker on personal VPS |
| Email | Resend (env wired, cert email path not implemented) |
| PDF | `pdf-lib` + `@napi-rs/canvas` + `qrcode` |
| Spreadsheet export | `exceljs` |
| Tests | Playwright e2e under `e2e/`, local-only |

## Trust boundaries (real)

- **Browser → Next.js API routes**: Supabase Auth session validated server-side. No RLS layer behind it.
- **Next.js API routes → Postgres**: TypeORM with privileged connection. Application code is the security boundary.
- **Next.js API routes → R2**: AWS SDK with R2 access keys server-side; clients only ever see presigned URLs.
- **Next.js API routes → WAHA**: HTTP with optional `WAHA_API_KEY`, sessions are long-lived and brittle.
- **Public → certificate verify**: `/api/public/certificates/pdf` accessible with `certificate_id`. Anyone with the ID can fetch the PDF. Acceptable per product intent (verify-by-QR).

## Cron jobs

| Route | Purpose | Status |
| --- | --- | --- |
| `/api/cron/files/cleanup-expired` | delete or hide expired R2 materials | not scheduled in Vercel |
| `/api/cron/reminders/class` | 1-hour-before WhatsApp reminder window (cron 55–65 min before start) | not scheduled in Vercel |

`CRON_SECRET` env exists; the **schedule entries themselves are missing** from `vercel.json` / project config. See backlog [[Projects/aksara-karir/backlog/p0-cron-reminders-fix]].

## Dev-only routes / surfaces

- `src/app/api/dev/db-ping` — DB ping
- `src/app/dev/*` — internal admin/debug pages
- `src/app/enterprise/*` — **hidden stub** for future B2B; not linked from nav

## Repository layout

- App: `~/Project/aksara-karir-lms` (local clone). Production tracks `main`.
- Technical docs submodule: `Projects/aksara-karir/docs/` ↔ https://github.com/MG177/aksara-karir-lms-docs (vault hub: same folder, `MOC.md` + `context/` etc.).
- WAHA stack: `docker-compose.waha.yml` (port 3001 to keep 3000 for Next).

## Gaps not yet covered in `docs/`

- Backups, observability, secrets rotation strategy — none documented because none implemented.
- Billing/account ownership — held entirely by mg's personal accounts; not in repo docs by design.
- Commercial / pricing / handover plan — vault-only.
