---
name: ai-project-context
description: >-
  Sets up a six-file project context pack plus an agent entry file so coding
  agents stay consistent across sessions. Use when starting a new app with an
  AI coding agent, or when the user asks to generate project context files,
  CLAUDE.md, AGENTS.md, or a six-file context system before writing code.
  Also use when updating existing context files after a scope, architecture,
  or progress change — do not regenerate all six files unless starting fresh.
---

# AI project context

Create or update a durable context pack the coding agent reads before it implements anything. You are writing project truth, not scaffolding. Fill every file for this specific product. Do not leave placeholder brackets, and do not invent product behavior, stack choices, or visual design the user has not agreed to.

## Modes

**New project.** Generate all six context files and one entry file, tailored to the current request.

**Existing project.** If `context/` (or the project's existing context folder) already has these files, read them first. Update only the files that the change actually affects, almost always including `progress-tracker.md`. Do not regenerate the whole pack from scratch.

Do not start implementing application code unless the user asked for that in the same request.

## 1. Gather enough thinking first

Before writing files, you must be able to answer:

- What the app does in one sentence, who it is for, and the core user flow
- What is in scope for v1 and what is explicitly out of scope
- Stack and why, where data lives, and how auth / ownership works
- Visual language, or that UI is undecided
- The first buildable units and their order

If the user already provided this, do not re-ask. If important decisions are still open, ask focused questions and push back on vague answers. Record unresolved items in `progress-tracker.md` under Open Questions rather than guessing.

When a choice is needed and the user did not specify one, state the recommended default in the relevant file and label it as a recommendation, not a fact.

## 2. Choose where the files go

Default layout at the project root:

```
AGENTS.md
context/
├── project-overview.md
├── architecture.md
├── code-standards.md
├── ai-workflow-rules.md
├── ui-context.md
└── progress-tracker.md
```

- Use `AGENTS.md` as the default entry file (Cursor, Codex, and many other agents read it).
- If the user uses Claude Code, also write `CLAUDE.md` with the same body.
- If `CLAUDE.md`, `AGENTS.md`, or a Cursor rules file already exists, update it so it points at these context files. Do not delete unrelated existing rules.
- If the repo already keeps docs in another folder (`docs/context/`, etc.), follow that convention instead of creating a second pack.
- Confirm the destination if writing into an existing repo would overwrite files.

## 3. Write the files

Every file must be specific and concrete. Measurable goals, step-by-step flows, named folders, and rules written as commands, not soft suggestions.

### `context/project-overview.md`

What you are building and why.

- Overview (one paragraph)
- Goals (numbered, measurable)
- Core user flow (step by step, no gaps)
- Features, grouped by category
- In scope / out of scope (out of scope must be explicit)
- Success criteria (verifiable, not "looks good")

### `context/architecture.md`

How the system fits together. This is the most important file.

- Stack table: layer, technology, role
- System boundaries: which folder owns which responsibility
- Storage model: database vs files/blob vs cache
- Auth and access model: sign-in, ownership, who can mutate what
- Invariants: at least four rules the codebase must never violate

### `context/code-standards.md`

Conventions the agent must follow so later units match earlier ones.

- General principles
- Language/type rules
- Framework conventions
- Styling rules (tokens, not one-off values)
- API route rules (validate input, enforce auth before mutations, consistent responses)
- Data and storage rules
- File organization

### `context/ai-workflow-rules.md`

How the agent should work, written as direct rules.

- Spec-driven, incremental approach
- One feature unit at a time; no speculative extras
- When to split work (unrelated boundaries, unverifiable scope)
- Do not invent missing requirements; resolve them in context files or add an open question before coding
- Protected files the agent must not edit unless asked
- Keep context files in sync when implementation changes architecture, scope, or standards
- Checklist before the next unit: the current unit works end to end, no invariant was broken, progress tracker is updated, and the project build/test command passes

### `context/ui-context.md`

Visual decisions so the agent does not invent a new look each time.

- Theme / visual language
- Color tokens (semantic names + values; no raw hex in components)
- Typography
- Border radius scale
- Component library and where components live
- Layout patterns (shell, sidebars, modals, nav)
- Icon rules

If the visual system is not decided, ask or document only what is known and list the rest as open questions. Do not fabricate a complete brand.

### `context/progress-tracker.md`

The session memory file. Update it after every meaningful implementation change.

- Current phase
- Current goal
- Completed / in progress / next up
- Open questions
- Architecture decisions, with why
- Session notes needed to resume later

For a new pack, seed the first unit under Next Up and leave Completed empty unless work already exists.

### Entry file

The entry file must tell the agent to read the context files in this order before implementing or making architectural decisions:

1. `context/project-overview.md`
2. `context/architecture.md`
3. `context/ui-context.md`
4. `context/code-standards.md`
5. `context/ai-workflow-rules.md`
6. `context/progress-tracker.md`

It must also say: update `progress-tracker.md` after each meaningful change; if implementation changes architecture, scope, or standards, update the relevant context file before continuing.

## 4. Report

When the pack is written or updated, tell the user:

- Which files were created or changed, and where
- Any open questions still blocking implementation
- The first unit you recommend building

Then stop, unless the user asked you to start building.
