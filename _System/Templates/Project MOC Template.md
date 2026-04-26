---
id: moc-{{date:YYYY-MM-DD}}-{{title}}
type: moc
project: {{title}}
status: active
owner:
created: {{date:YYYY-MM-DD}}
updated: {{date:YYYY-MM-DD}}
tags: [type/moc, project/{{title}}]
links: []
---

# {{title}} - MOC

## TL;DR

One to three sentences summarizing the project outcome, current status, and the single next milestone. Written so an LLM can answer "what is this project?" from this section alone.

## Outcome

- Problem:
- Desired outcome:
- Success metric:
- Scope (in):
- Scope (out):

## Status

- Current phase:
- Next milestone:
- Target date:
- Health: green | yellow | red

## Quick Links

- Project context: [[Projects/{{title}}/context/index]]
- Technical docs (if `docs/` present): [[Projects/{{title}}/docs/README]]
- Decisions: [[Projects/{{title}}/decisions/index]]
- Changelog: [[Projects/{{title}}/changelog/index]]
- Backlog: [[Projects/{{title}}/backlog/index]]
- Meetings: [[Projects/{{title}}/meetings/index]]
- Runbooks: [[Projects/{{title}}/runbooks/index]]

## Project folders (what goes where)

| Folder | Use for | Do not use for |
|--------|---------|----------------|
| **`context/`** | Client, commercial, onboarding, handover, short vault-side system summary; hub **`context/index.md`**. | Technical specs duplicated from the repo — link to **`docs/README`** instead. |
| **`docs/`** (when present) | Technical / product docs with the codebase (architecture, data model, APIs, tests). Hub **`docs/README.md`**. | Client notes, ADRs, backlog — use `context/`, `decisions/`, `backlog/`. |
| **`decisions/`** | ADRs and dated “we chose X” records. | Operator procedures or task lists. |
| **`runbooks/`** | Repeatable ops procedures. | Product requirements or ADR rationale. |
| **`backlog/`** | Prioritized work and owners. | Long-form reference docs. |
| **`meetings/`** | Meeting-specific notes. | Evergreen architecture writeups. |
| **`changelog/`** | Dated narrative of what changed in the vault or project story. | Git history by default. |
| **`archive/`** | Superseded notes. | Active work. |

**One-line test:** if every open task and meeting disappeared, would this note still help someone understand the project? If yes → **`context/`** or **`docs/`** (technical); choice records → **`decisions/`**; “when X happens, do Y” → **`runbooks/`**.

## Open Decisions

- [ ] [[Projects/{{title}}/decisions/adr-YYYY-MM-DD-slug]] - short question

## Active Backlog

- [ ] [[Projects/{{title}}/backlog/slug]] - p0 | p1 | p2 - owner

## Recent Changes

- {{date:YYYY-MM-DD}} - [[Projects/{{title}}/changelog/YYYY-MM-DD-slug]] - one-line summary

## Risks & Blockers

- Risk: | Impact: | Mitigation: | Owner:

## Next Actions

- [ ] Action - owner - due YYYY-MM-DD

## Related

- [[Resources/]]
- [[Areas/]]
