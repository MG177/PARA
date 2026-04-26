# AGENTS.md

Operational guide for coding agents in this workspace.

## Scope

- Workspace root is `PARA/` with top-level folders: `Areas/`, `Inbox/`, `Projects/`, `Resources/`, `Temp/`, `_Archive/`, `_System/`.
- Treat this as a mixed workspace (notes + projects). Confirm target path before creating or moving files.
- **Obsidian project hubs:** feature or app work under `Projects/<name>/` should index the vault via **`MOC.md`** in that folder—not a duplicate `Projects/<name>.md`. Link areas with `area:` / `area/…` tags. Dashboard Dataview must use **`regexmatch(pattern, field)`** (pattern first). Folder layout: **`context/`** = vault-side client/onboarding/commercial notes (hub `context/index.md`); **`docs/`** = technical/product markdown with the code (when present). Full rules: `.cursor/rules/moc-project-structure.mdc`.

## Path Discipline

- Prefer project work under `Projects/` unless user specifies a different location.
- Do not reorganize PARA folders unless explicitly requested.
- Before writing new files, verify parent directory exists.
- Treat `_System/Templates/` as the canonical Obsidian template directory.
- Do not create duplicate template files outside `_System/Templates/` unless user explicitly requests a local override.
- For **template CLI automation**, use Obsidian’s **official CLI** (`templates`, `template:read`, `template:insert`, `create … template=…`, plus `commands` / `command` for Templater): app must be running; full parameter table and scope (core vs Templater) live in `.cursor/rules/obsidian-template-usage.mdc`.

## Temp Output Rule

- Use `Temp/` for large, generated, or ephemeral artifacts.
- Do not read/search `Temp/` unless user explicitly asks or references a file there.
- Do not treat files in `Temp/` as canonical configuration or documentation.

## Command Constraints

- Do not run `eslint` commands.
- Do not run project build commands (`build`, `next build`, `tsc --build`, etc.).
- Prefer targeted validation (typecheck/tests for changed scope) only when requested or clearly necessary.

## Editing Safety

- Never revert unrelated user changes.
- Avoid destructive git operations (`reset --hard`, forced checkout) unless user explicitly requests them.
- Keep edits minimal and scoped to the request.

## Communication Style

- Be direct, terse, and implementation-first.
- Prefer concrete code/patches over high-level advice.
- For explanations, include exact paths and actionable details.
