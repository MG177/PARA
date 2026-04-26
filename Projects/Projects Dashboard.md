---
type: dashboard
created: 2026-04-26
tags: [projects, dashboard]
---

# Projects Dashboard

Project hubs are **either** a root note `Projects/<Name>.md` **or** a folder index `Projects/<Name>/MOC.md` (not both — avoid duplicating the name). Capture raw ideas in [[Projects/Project Intake]] first, then promote using [[_System/Templates/Project Template]] or [[_System/Templates/Project MOC Template]].

**Statuses:** `active` · `waiting` · `on-hold` · `done` — set `completed: YYYY-MM-DD` when marking `done` so the “Completed recently” table sorts correctly.

## Quick Links

- [[Projects/Project Intake]] — inbox before a project exists
- [[_System/Templates/Project Template]] — new hub note
- [[Projects/aksara-karir/MOC]] — LumenDev / Aksara Karir LMS
- [[Client Proposal Upgrade]]
- [[Planning scratch]]

## Active Projects

```dataview
TABLE status, due, created, tags
FROM "Projects"
WHERE (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND status = "active"
SORT due ASC, created DESC
```

## Active — no due date

```dataview
TABLE status, created, tags
FROM "Projects"
WHERE (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND status = "active"
  AND !due
SORT created DESC
```

## On Hold / Waiting

```dataview
TABLE status, due, created
FROM "Projects"
WHERE (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND (status = "waiting" OR status = "on-hold")
SORT created DESC
```

## Needs status

Hub notes missing `status` in frontmatter (fix or archive):

```dataview
TABLE file.mtime as "Modified"
FROM "Projects"
WHERE (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND !status
SORT file.mtime DESC
```

## Completed Recently

```dataview
TABLE completed, created
FROM "Projects"
WHERE (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND status = "done"
SORT completed DESC
LIMIT 10
```

## Open Tasks (hub notes only)

Tasks on root `Projects/*.md` hubs and on `Projects/<project>/MOC.md` only (not `docs/` trees):

```dataview
TASK
FROM "Projects"
WHERE (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND !completed
SORT file.name ASC
```
