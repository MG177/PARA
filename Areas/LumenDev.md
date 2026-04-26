---
type: area-dashboard
area: lumendev
created: 2026-04-26
tags: [areas, dashboard, area/lumendev]
---

# LumenDev

Software house — ongoing business area.

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
  AND status = "done"
SORT completed DESC
LIMIT 10
```

## Open tasks (linked projects)

```dataview
TASK
FROM "Projects"
WHERE area = "lumendev"
```

---

## Hub

- [[Projects/Projects Dashboard]]
- [[Projects/Project Intake]]
- [[Home]]
