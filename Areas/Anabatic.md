---
type: area-dashboard
area: anabatic
role: Software Developer
created: 2026-04-26
tags: [areas, dashboard, area/anabatic]
---

# Anabatic

Employment area — software development (PT Anabatic Tbk).

## Link projects here

On any project note under `Projects/`, set frontmatter:

- `area: anabatic`  
  or tag: `area/anabatic`

---

## Active projects

```dataview
TABLE status, due, created, tags
FROM "Projects"
WHERE type != "dashboard"
  AND file.name != "Project Intake"
  AND area = "anabatic"
  AND status = "active"
SORT due ASC, created DESC
```

## Waiting / on hold

```dataview
TABLE status, due, created
FROM "Projects"
WHERE type != "dashboard"
  AND file.name != "Project Intake"
  AND area = "anabatic"
  AND (status = "waiting" OR status = "on-hold")
SORT created DESC
```

## Recently completed

```dataview
TABLE completed, created
FROM "Projects"
WHERE type != "dashboard"
  AND file.name != "Project Intake"
  AND area = "anabatic"
  AND status = "done"
SORT completed DESC
LIMIT 10
```

## Open tasks (linked projects)

```dataview
TASK
FROM "Projects"
WHERE area = "anabatic"
```

---

## Hub

- [[Projects/Projects Dashboard]]
- [[Projects/Project Intake]]
- [[Home]]
