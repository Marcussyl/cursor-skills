---
name: commit-batches
description: >-
  Commits the working tree in several focused commits, each containing only
  related changes, then pushes to the remote. Use when the user invokes
  /commit-batches, asks to commit in batches, split commits, or batch commits
  by topic.
disable-model-invocation: true
---

# Commit in batches

Split uncommitted work into logical commits. Each commit should be reviewable on its own and include every file needed for that slice to make sense.

## Safety (always)

- Never update git config.
- Never force-push, hard reset, or other destructive git unless the user explicitly asks.
- Never skip hooks (`--no-verify`, etc.) unless the user explicitly asks.
- Never stage secrets (`.env`, credentials, keys). Warn and exclude them.
- Never use `git commit --amend` unless the user rules for amend are fully met.
- If a commit hook fails, fix the issue and create a **new** commit; do not amend a failed commit.
- Do not add `Co-authored-by: Cursor` to commit messages.

## 1. Inspect

Run in parallel when possible:

- `git status`
- `git diff` and `git diff --staged`
- `git log -5 --oneline` for message style
- `git remote -v` and branch tracking (`git status -sb`)

If there is nothing to commit, stop and say so.

## 2. Plan batches

Group changes by **purpose**, not by file type alone. Examples:

- One feature or user-facing behavior + its tests and docs
- One bug fix + only the files that fix it
- Refactor that stands alone without mixing unrelated features
- Chore or tooling scoped to one area (deps, CI, config)

Rules:

- Do not mix unrelated features in one commit.
- Include companion files in the same batch (e.g. schema + entity + migration + call sites for one change).
- If a file touches two concerns, prefer the dominant batch or mention the tradeoff before committing.
- List batches in order: foundations first (shared types, config), then features, then docs-only if they depend on prior commits.

Show the user a short plan: batch number, files or paths, proposed conventional commit subject. Then proceed unless they object.

## 3. Commit each batch

For **each** batch, sequentially:

1. Stage **only** that batch (`git add` specific paths; avoid `git add -A` unless the whole tree is one batch).
2. Re-check with `git diff --staged` that nothing unrelated slipped in.
3. Write a **Conventional Commit** subject (`feat`, `fix`, `chore`, `docs`, `refactor`, `test`, etc.) focused on **why**.
4. If the branch name contains an issue id, append `#<issue>` to the subject (GitLab-style).
5. Commit. On Windows PowerShell, use `git commit -m 'subject'` (or multiple `-m` for a short body). On bash, a HEREDOC for the message is fine.
6. Repeat until the working tree is clean for intended changes.

## 4. Push to GitHub (or remote)

After all batches:

- If `origin` (or the user's named remote) exists and the branch should be published, run `git push -u origin HEAD` when upstream is missing, otherwise `git push`.
- Never force-push `main` or `master`.
- If push is rejected, report the error and suggest pull/rebase; do not force unless the user explicitly requests it.
- If there is no remote, say commits are local only and ask whether to add a remote.

## 5. Report

Summarize:

- Each commit hash and subject (newest last or numbered list).
- Push result (URL or branch if available).
- Anything left unstaged on purpose (secrets, local-only files).

## Relation to `commit-msg`

`commit-msg` suggests one line from **already staged** files and does not commit. This skill **plans, stages, commits in multiple steps, and pushes**.
