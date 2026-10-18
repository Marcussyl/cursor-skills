---
name: commit-msg
description: Suggest one conventional commit line from staged files. Use when invoked via /commit-msg.
disable-model-invocation: true
---

# Commit message

Use this only when the user invokes `/commit-msg`.

1. Inspect staged changes only. Do not run `git commit`.
2. If nothing is staged, stop and say so.
3. Reply with one Conventional Commit line that is easy to copy.
4. If the current branch name contains an issue number, append `#<issue>` to that line.
