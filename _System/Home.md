---
type: dashboard
---

# 🏠 Home

> [!tip] Daily Focus
>
> - [[_System/Start Here]]
> - [[Inbox/Inbox]]
> - [[_System/Weekly Review]]
> - [[Client Proposal Upgrade]]

---

## Areas

- [[Areas/Anabatic]] — employment
- [[Areas/LumenDev]] — software house

---

## 🎯 This Week

- [ ] Review active projects
- [ ] Clear inbox
- [ ] Run weekly review

## 🚀 Active Projects

```dataview
TABLE WITHOUT ID
file.link AS Project,
status AS Status,
due AS Due,
next_action AS "Next Action"
FROM "Projects"
WHERE type = "project" AND status = "active"
SORT due ASC
```

## ⏳ Waiting

```dataview
TABLE WITHOUT ID
file.link AS Project,
owner AS Owner,
due AS Due
FROM "Projects"
WHERE status = "waiting"
SORT due ASC
```

## 📝 Recent Notes

```dataview
TABLE WITHOUT ID
file.link AS Note,
dateformat(file.mtime, "ccc, dd LLL • HH:mm") AS Updated
FROM ""
SORT file.mtime DESC
LIMIT 12
```
