---
type: area-dashboard
area: lumendev
created: 2026-04-26
tags: [areas, dashboard, area/lumendev]
---

# LumenDev

Software house — ongoing business area.

## Client & product hubs

- [[Projects/aksara-karir-hub/MOC]] — Aksara Karir LMS (vault hub; technical docs submodule at `Projects/aksara-karir/`)

## Link projects here

On any project note under `Projects/`, set frontmatter:

- `area: lumendev`  
  or tag: `area/lumendev`

---

## Active projects

```dataview
TABLE status, due, created, tags
FROM "Projects"
WHERE type != "dashboard"
  AND file.name != "Project Intake"
  AND area = "lumendev"
  AND (
    (file.folder = "Projects" AND file.name != "Projects Dashboard")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND status = "active"
SORT due ASC, created DESC
```

## Waiting / on hold

```dataview
TABLE status, due, created
FROM "Projects"
WHERE type != "dashboard"
  AND file.name != "Project Intake"
  AND area = "lumendev"
  AND (
    (file.folder = "Projects" AND file.name != "Projects Dashboard")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND (status = "waiting" OR status = "on-hold")
SORT created DESC
```

## Recently completed

```dataview
TABLE completed, created
FROM "Projects"
WHERE type != "dashboard"
  AND file.name != "Project Intake"
  AND area = "lumendev"
  AND (
    (file.folder = "Projects" AND file.name != "Projects Dashboard")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND status = "done"
SORT completed DESC
LIMIT 10
```

## Open tasks (linked projects)

```dataview
TASK
FROM "Projects"
WHERE area = "lumendev"
  AND (
    (file.folder = "Projects" AND file.name != "Projects Dashboard" AND file.name != "Project Intake")
    OR (file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder))
  )
  AND !completed
```

---

## Hub

- [[Projects/Projects Dashboard]]
- [[Projects/Project Intake]]
- [[Home]]
