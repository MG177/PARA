---
type: dashboard
created: 2026-04-26
tags: [projects, dashboard]
---

# Projects Dashboard

## Quick Links

- [[Projects/Project Intake]]
- [[_System/Templates/Project Template]]
- [[Client Proposal Upgrade]]
- [[Planning scratch]]

## Active Projects

```dataview
TABLE status, due, created, tags
FROM "Projects"
WHERE type != "dashboard" AND file.name != "Project Intake" AND status = "active"
SORT due ASC, created DESC
```

## On Hold / Waiting

```dataview
TABLE status, due, created
FROM "Projects"
WHERE type != "dashboard" AND file.name != "Project Intake" AND (status = "waiting" OR status = "on-hold")
SORT created DESC
```

## Completed Recently

```dataview
TABLE completed, created
FROM "Projects"
WHERE type != "dashboard" AND file.name != "Project Intake" AND status = "done"
SORT completed DESC
LIMIT 10
```

## Open Tasks Across Projects

```dataview
TASK
FROM "Projects"
WHERE !completed
SORT file.name ASC
```
