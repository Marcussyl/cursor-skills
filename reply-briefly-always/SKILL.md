---
name: reply-briefly-always
description: >-
  Turn on brief Chinese replies for the rest of the chat. Use when the user
  invokes /reply-briefly-always or asks to keep /replay-briefly style for the
  whole conversation.
disable-model-invocation: true
---

# Reply briefly (always)

Invoke once per chat. After that, **every following reply** in this conversation uses the same **Reply** rules as `replay-briefly` (see `replay-briefly/SKILL.md`).

## Activate

User says `/reply-briefly-always` or clearly asks to keep brief replies for the rest of the conversation.

Confirm in one short sentence that brief mode is on for this chat.

## Reply (every turn until user turns it off)

Reply in short Chinese:

- Put the answer in the first one or two sentences.
- Add detail only when it changes what the user should do.
- End with **In short** in one or two sentences.
- Skip long background and long menus of options.

## How this differs from /replay-briefly

| | `replay-briefly` | `reply-briefly-always` |
|---|------------------|------------------------|
| Scope | Single invocation (unless user repeats) | Rest of **this** chat |
| Answer-only | Yes — no edits or git writes | **No** — only **style**; normal Agent work still allowed when the user asks |

Do **not** apply `replay-briefly`'s answer-only restrictions for the whole chat unless the user also invokes `/replay-briefly` on that turn.

## Turn off

User says they want normal length, turn off brief mode, or stop using replay style for the session.

## Allowed

- Read, search, explain, and implement when the user requests changes.
- Follow brief reply format even while editing or running commands.

## Not allowed

- Silently dropping brief format after activation.
- Treating this skill as answer-only by default.
