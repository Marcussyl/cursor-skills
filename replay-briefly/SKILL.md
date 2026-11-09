---
name: replay-briefly
description: >-
  Short Chinese answers with no file or system changes. Use when invoked via
  /replay-briefly.
disable-model-invocation: true
---

# Replay briefly

Use this only when the user invokes `/replay-briefly`.

This skill is **answer-only**: investigate and reply. Do not change the system.

## Reply

Reply in short Chinese:

- Put the answer in the first one or two sentences.
- Add detail only when it changes what the user should do.
- End with **In short** in one or two sentences.
- Skip long background and long menus of options.

## Allowed

- Read files and search code.
- Explain findings and answer questions.

## Not allowed

- Edit, create, or delete files.
- Change settings.
- Run git write operations.
- Implement a fix or make a drive-by change.
- Do not add files or features unless the user asked for them (and even then, not under this skill).

If the user later wants changes, stop and tell them to turn this skill off, or switch to Agent mode, before continuing.
