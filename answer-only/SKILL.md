---
name: answer-only
description: >-
  Answers like Ask mode with no file or system changes. Use when the user
  invokes this skill, asks not to change anything, or wants an answer-only
  investigation.
---

# Answer only

Investigate and explain. Do not change the system.

## Allowed

- Read files and search code.
- Explain findings and answer questions.

## Not allowed

- Edit, create, or delete files.
- Change settings.
- Run git write operations.
- Implement a fix or make a drive-by change.

If the user later wants changes, stop and tell them to turn this skill off, or switch to Agent mode, before continuing.
