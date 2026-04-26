---
type: runbook
project: aksara-karir
status: active
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/runbook, project/aksara-karir, whatsapp, ops]
---

# Runbook — WAHA session restart

## TL;DR

Restart and re-pair the WAHA WhatsApp session when scheduled WA messages stop sending. This is currently the #1 operational toil.

## Scope

- Applies to the WAHA Docker container running on the personal VPS used for prod.
- Symptom: scheduled reminders or admin-triggered WhatsApp messages silently fail; `/api/admin/waha/health` reports session not active.

## Preconditions

- SSH access to the VPS.
- Admin login to the LMS (to scan QR via Admin → Messages panel) — sessions can also be paired via WAHA's own dashboard if exposed.
- Phone with the bound WhatsApp number reachable for QR scan.

## Procedure

1. Confirm symptom: open Admin → Messages in the LMS and check session health. Or hit `GET /api/admin/waha/health` directly.
2. SSH to the VPS.
3. Inspect the WAHA container:
   ```bash
   docker compose -f docker-compose.waha.yml ps
   docker compose -f docker-compose.waha.yml logs --tail=200 waha
   ```
4. If the container is unhealthy, restart:
   ```bash
   docker compose -f docker-compose.waha.yml restart waha
   ```
   If config changed, do `down` then `up -d`.
5. Re-pair the session via Admin → Messages → WAHA panel (QR view) or directly via WAHA's dashboard:
   - Get a fresh QR.
   - On the WhatsApp app on the bound phone: Settings → Linked devices → Link a device → scan.
6. Send a test message from Admin → Messages or via `POST` to a WAHA send endpoint to confirm.

## Rollback

- N/A — restart is non-destructive.
- If repeated restarts within a day → suspect WhatsApp ban; do **not** keep sending. Pause cron, escalate to ADR review (Meta Cloud API migration).

## Validation

- `GET /api/admin/waha/health` returns active.
- Test message delivered.
- Cron logs show next reminder sent at the expected time.

## Related Incidents

- Recurring; logged informally in WhatsApp chat with client. To be tracked formally once an issue tracker exists.

## References

- [[Projects/aksara-karir/decisions/adr-2026-04-26-waha-vs-meta-cloud-api]]
- `docker-compose.waha.yml` in repo root.
