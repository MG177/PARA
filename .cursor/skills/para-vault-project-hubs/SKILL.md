---
name: para-vault-project-hubs
description: >-
  When adding feature projects, client repos, or app folders under Projects/, wiring
  them to Areas (e.g. LumenDev), or writing Dataview on Projects/Areas dashboards.
---

# PARA vault project hubs

Canonical spec: **`.cursor/rules/moc-project-structure.mdc`** (always on). **`.cursor/rules/moc-project-operations.mdc`** for day-to-day MOC edits under a project folder.

## Do this

1. **Folder project (features, clones, docs trees)** — `Projects/<slug>/` with **`MOC.md`** at that root as the **only** Obsidian index for that slug. Link into **`context/`** (vault narrative), **`docs/`** (technical repo mount when present), `decisions/`, etc. See **`docs/` vs `context/`** in `.cursor/rules/moc-project-structure.mdc`. Never add `Projects/<slug>.md` alongside the same-named folder.
2. **Flat project** — only `Projects/<Slug>.md`; no `Projects/<Slug>/` folder with the same name.
3. **Dashboards** — on the hub file set `status`, optional `due` / `completed`, and `area: <slug>` (and/or `area/<slug>` tag) so [[Areas/LumenDev]]-style Dataviews match.
4. **Dataview** — hub union for folder MOCs must use **`regexmatch(pattern, field)`** (pattern first). Correct fragment:

   `file.name = "MOC" AND regexmatch("^Projects/[^/]+$", file.folder)`

   Reversing arguments excludes every folder project from tables. Reuse the same filter for `TASK` blocks so `docs/` does not flood tasks.

## Templates

- Flat hub: `_System/Templates/Project Template.md`
- Folder MOC (governance-heavy): `_System/Templates/Project MOC Template.md`

## In-repo pointers

- `AGENTS.md` (workspace root) — short reminder + link to `moc-project-structure.mdc`.
