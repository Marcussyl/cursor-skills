---
name: html-critical-path-test-guide
description: >-
  Produces a self-contained dark-theme HTML document with architecture diagrams,
  critical-path tables (exact function names), focused code review, API reference,
  and expandable manual QA scenarios. Use when the user asks for code review docs,
  critical path analysis, cross-repo test guides, QA checklists in HTML, or
  project-docs deliverables similar to payslip-keystore-code-review-and-test-guide.html.
---

# HTML critical-path code review & test guide

## When to use

Apply this skill when the user wants a **single offline HTML file** for engineers/QA that combines:

- Architecture / data-flow mental model
- **Critical paths** (P1, P2, …) with **exact** function, method, or route names
- Short **code review** (strengths + risks, not a line-by-line PR)
- **API / endpoint** table (if applicable)
- **Manual test guide** with checklists and `<details>` scenarios
- Optional **中文** summary lines (`p.zh`) for bilingual teams

Default output directory: **`{project-root}/project-docs/`** (local, usually gitignored).

## Before writing

1. **Confirm scope**: feature name, repos/paths (one or many workspaces), audience (dev vs QA).
2. **Investigate in the codebase** — do not invent paths or functions:
   - Ripgrep feature keywords (domain terms, plugin names, API segments).
   - Read entry points (UI gates, services, route handlers, native plugins).
   - Trace each user-visible flow to the leaf (DB, native bridge, external API).
3. **Prioritize paths** by user impact and security:
   - Label **Critical** = money, auth, crypto, PII, or irreversible actions.
   - Label **High** = recovery, alignment, admin.
   - Label **Medium** = bootstrap, diagnostics, empty states.
4. Ask the user before adding **new** test scenarios they did not imply if those scenarios need prod data or destructive steps.

## Output file rules

| Rule | Detail |
|------|--------|
| Format | One `.html` file, no external CSS/JS/assets |
| Naming | `{feature-slug}-code-review-and-test-guide.html` (kebab-case, English) |
| Location | `project-docs/` under the primary repo unless user specifies another path |
| Language | Section titles EN; add `p.zh` where the user prefers Chinese |
| Code refs | Use `<code>functionName</code>` and repo tags, not only prose |
| Print | Include `@media print` friendly rules (see template) |

Ensure the project `.gitignore` lists `project-docs/` when the user wants local-only docs.

## Required document sections (in order)

Use sticky TOC linking to these `id`s:

1. **`#architecture`** — 1 ASCII diagram + 2–4 sentences on trust boundaries (what never leaves device, what server stores).
2. **`#critical-paths`** — For each path **Pn**:
   - Table columns: Step | Repo/layer | Critical function(s) | Notes
   - Call chain **top → bottom** (caller before callee).
3. **`#function-map`** — Layer cards (e.g. native, mobile shell, web client, server).
4. **`#review`** — `.finding` blocks: at least one **ok** (strengths), 3–6 risks/regressions (concrete, not generic OWASP laundry lists).
5. **`#apis`** — If HTTP/RPC exists; else omit with a one-line “N/A — no public API surface”.
6. **`#testing`** — Global prerequisites + **T1…Tn** in `<details class="test-case">`:
   - Path ID reference (e.g. P2)
   - Preconditions
   - `ul.checklist` steps (☐ via CSS)
   - Expected results + common failure codes
7. **`#matrix`** — Path × surface × primary entry function × priority tag.

End with **source file index** (`<pre>` absolute or repo-relative paths).

## HTML structure & styling

Copy the shell from [html-shell-template.md](html-shell-template.md):

- CSS variables dark theme (`:root` colors, `.tag-critical`, `.finding`, `details.test-case`).
- `<header>` with title, subtitle, optional `.meta` (branch/date).
- `<nav class="toc">` sticky anchor links.
- `<main>` with `<section id="...">` panels.

Do **not** shrink the doc into markdown-only unless the user explicitly asks.

## Critical path authoring standards

Each path must answer:

1. **Who** triggers it (user action / cron / webhook)?
2. **What** is the first function in app code (not “the system”)?
3. **Where** does it cross repo or process (WebView, Cordova, second git repo)?
4. **What** error codes or states block progress?

Use consistent IDs: **P1**, **P2**, … and test IDs **T1**, **T2**, …

Link tests to paths: `Path: P1 · ensureFoo → barNative`.

## Code review block guidance

Keep review **scoped to the feature under documentation**:

- **Strengths**: security properties actually implemented in code (cite mechanism).
- **Risks**: mismatch between two gates, session caching, timeout vs missing plugin, contract drift between repos.
- **Regression watch**: shared constants, crypto suites, schema migrations.

Avoid claiming tests exist unless you verified test files.

## Multi-repo workflow

When paths cross repositories:

- Tag table cells with `.tag-repo-*` or plain repo short names.
- Search **each** workspace root the user named.
- In the matrix, split “Portal entry” vs “Companion entry” columns when useful.

## Installing this skill for Cursor

From [Marcussyl/cursor-skills](https://github.com/Marcussyl/cursor-skills):

```bash
ln -sf "$HOME/.cursor/skills-repo/html-critical-path-test-guide" \
  ~/.cursor/skills/html-critical-path-test-guide
```

(Adjust `skills-repo` to your clone path.) Restart Cursor or start a new agent thread after adding.

## Quality checklist (agent self-verify)

- [ ] Every Pn path has ≥3 steps with real function names from the repo
- [ ] At least one test per Critical path
- [ ] APIs match actual route files or OpenAPI
- [ ] No broken internal links in TOC
- [ ] File opens correctly in browser (valid HTML5, escaped `&` in titles)
- [ ] User-requested output path used; `project-docs` exists

## Example user prompts

- “Code review for X, critical paths and HTML test guide in project-docs.”
- “Cross-repo doc for feature Y like the payslip keystore HTML.”
- “QA checklist HTML for authentication flow in epayroll + companion app.”
