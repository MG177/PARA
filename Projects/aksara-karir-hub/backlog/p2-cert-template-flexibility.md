---
id: p2-cert-template-flexibility
type: backlog
project: aksara-karir
status: ready
priority: p2
owner: mg
created: 2026-04-26
updated: 2026-04-26
tags: [type/backlog, project/aksara-karir, certificates]
---

# Backlog: Flexible certificate templates

## TL;DR

Client wants per-course or per-batch certificate templates (different background, signatures, layouts). Current generation is hardcoded.

## Description

- Define a template format: probably an SVG / PNG background + a JSON layout describing text fields, fonts, positions, QR placement.
- Store templates in R2; reference by `t_courses.certificate_template_id` (or per-batch override).
- Admin UI to upload background + edit layout.
- Generation pipeline reads layout, composites with `pdf-lib` / `@napi-rs/canvas`.
- Versioning so existing certificates remain reproducible if a template changes.

## Acceptance Criteria

- [ ] Schema migration for template references.
- [ ] At least 2 distinct templates rendered correctly side-by-side.
- [ ] Admin can upload + preview a new template without code changes.
- [ ] Existing certificate IDs still verify and re-render with their original template version.

## Priority

- Priority: p2
- Rationale: explicit client request, but not blocking operations.

## Dependencies

- Related: [[Projects/aksara-karir-hub/backlog/p2-cert-email-resend-impl]]

## Links

- [[Projects/aksara-karir/features/feat-certificates]]
