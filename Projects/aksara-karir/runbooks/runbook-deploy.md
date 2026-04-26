---
type: runbook
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/runbook, project/aksara-karir, deploy]
---

# Runbook — Deploy to production

## TL;DR

Deploys are direct: push to `main`, Vercel auto-builds and promotes. There is no staging. Run Playwright e2e locally before pushing.

## Scope

- Production deploys of the Next.js app.
- Does **not** cover WAHA, Supabase schema, R2 bucket settings — those are managed out-of-band.

## Preconditions

- Local repo at `~/Project/aksara-karir-lms`, on `main`.
- Local `.env` matches prod env values for any SDKs that need it during build.
- `npx playwright install` already run at least once.

## Procedure

1. Pull latest:
   ```bash
   git pull --rebase origin main
   ```
2. Run e2e locally:
   ```bash
   npm run test:e2e
   ```
   All specs must pass.
3. Optional: build locally to catch TypeScript errors before Vercel does.
4. Commit and push:
   ```bash
   git push origin main
   ```
5. Watch the Vercel dashboard until the deployment is `Ready`.
6. Smoke check prod:
   - Open homepage.
   - Log in as admin.
   - Hit `/api/admin/waha/health`.

## Rollback

- In Vercel dashboard → Deployments → previous successful one → **Promote to Production**. No DB migration is involved by default; if a migration was applied, see schema-rollback notes (TBD).

## Validation

- Vercel build status: success.
- Smoke checks pass.
- No new errors in browser console / Vercel logs for 10 minutes.

## Related Incidents

- TBD.

## References

- `.env` and `.env.example` for required env values.
- [[Projects/aksara-karir/backlog/p1-staging-environment]]
