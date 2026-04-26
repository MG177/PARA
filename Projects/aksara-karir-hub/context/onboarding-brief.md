---
type: documentation
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/documentation, project/aksara-karir, onboarding]
---

# Aksara Karir — Onboarding Brief

## TL;DR

Single-source onboarding doc for any developer or operator picking up Aksara Karir. Captures client, users, product behavior, ops reality, commercial frame, and known risks not documented in the in-repo `docs/` submodule.

## Client snapshot

- Legal client: **Aksara Karir** — Indonesian online learning company, niche in **mining and geology**.
- Format: live **Zoom** courses + recordings; sells **certificates of completion**.
- Maturity: **new business**, income still inconsistent, no PT/CV legal entity yet (blocks payment gateway adoption).
- Vendor relationship: **Lumen Dev** delivered as **one-time project**. No retainer or SLA in place. Comms via **WhatsApp**, no formal ticketing.

## Users in reality

- **Three personas in PRD/docs** (Student Learner, Professional Learner, Administrator) but in the **app today** Student and Professional are treated **identically** — same flow, same pricing logic, same UI. Difference is marketing only.
- **B2C only** today. B2B (corporate HR enrolls cohort) is a backlog feature; the `src/app/enterprise/` route exists as **hidden stub**, not exposed to users.
- **Admin: one shared account** held by Aksara staff. No per-user audit trail.

## Product behavior worth knowing

- **Registration:** user registers once with WA + email + name + company/school + job title. Pays via **manual bank transfer**, uploads payment proof on registration; admin verifies in dashboard.
- **Schedule:** dashboard cards in WIB/WITA/WIT, "Join" button activates 15 min before class, redirects to Zoom. Add-to-Google-Calendar one-click.
- **Reminders:** 1-hour-before WhatsApp message via WAHA. **Cron route exists in code but not scheduled in Vercel** — feature silently broken in prod.
- **Files / recordings:** uploaded by **Aksara staff** themselves. Stored in **Cloudflare R2**, served via presigned URLs (`/api/files/stream`, `/api/files/multipart`), with `expiration_date` per material; expired files return 403. **No garbage collection** — orphaned blobs accumulate.
- **Certificates:** admin marks user "Completed" (manual, based on Aksara's external attendance system — not integrated). PDF generated server-side (`pdf-lib` + `@napi-rs/canvas` + `qrcode`). Verification via public `/api/public/certificates/pdf` keyed by `certificate_id` + QR code. **Resend email delivery: not implemented** (env wired, code path absent).
- **Attendance:** admin's external system, not integrated. We trust admin's manual completion mark.
- **Retake:** not allowed; one registration per (user, course-batch).

## Stack

- **Next.js 16** (App Router) + **React 19**, deployed on **Vercel** (auto-deploy from `git push`, no preview env, no staging).
- **Supabase** — Auth (email + password only) and **PostgreSQL** (no RLS today).
- **TypeORM** for direct DB access from API routes (bypasses PostgREST).
- **Cloudflare R2** via `@aws-sdk/client-s3` and `@aws-sdk/s3-request-presigner` (presigned + multipart).
- **WAHA** (unofficial WhatsApp HTTP API) running in **Docker on a personal VPS**.
- **Resend** for email (env wired, cert email not yet built).
- **Playwright** e2e suite under `e2e/`, run **locally only**, no CI.
- **pdf-lib + napi-rs/canvas** for cert PDF rendering.
- **exceljs** for `GET /api/admin/courses/[id]/export-attendees`.

## Ops reality

- **Single owner of prod access (mg).** Co-developer (friend) is fallback but not yet provisioned with credentials.
- **All accounts and billing on mg's personal credit card**: Vercel, VPS (WAHA), Supabase, Cloudflare R2, Resend, domain.
- **No backups** (Supabase PITR off, R2 versioning off).
- **No monitoring or logging** beyond Vercel default; outages discovered when client WAs us.
- **No staging environment.** Push to `main` = prod.
- **Secrets not rotated** since project start.
- **Deploy gate:** "Playwright e2e passes locally" (manual, every push to prod).

## Top operational pain points (current, ranked)

1. **WAHA session drops silently** — must be restarted and QR re-scanned. Risk of WA number ban escalates with frequency. See [[Projects/aksara-karir-hub/runbooks/runbook-waha-session-restart]].
2. **R2 garbage** — no GC, files must be deleted by hand, bill grows linearly.
3. **Certificate template inflexibility** — client wants per-course / per-batch templates; not designed for it yet.

## Commercial frame

- One-time project complete. No renewal, no SLA, no signoff.
- Plan: pitch a **subscription / retainer** to take over ops + incremental features. See [[Projects/aksara-karir-hub/context/commercial]] for proposed structure.
- Aksara is **cash-strained**; pricing must reflect that without subsidizing infra costs out of pocket forever.

## Where to read more

- In-repo product docs (canonical): [[Projects/aksara-karir/README]]
- Architecture: [[Projects/aksara-karir/architecture/arch-overview]]
- Data model: [[Projects/aksara-karir/data-model/data-overview]]
- Features: [[Projects/aksara-karir/features/feat-prd-summary]]
- Initial PRD (Notion): https://www.notion.so/2e8bdcdd44cd80a496ebfa0f467cf493
