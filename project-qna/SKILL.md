---
name: project-qna
description: >-
  Writes a project Q&A as a single QnA.html file under the project's
  project-docs folder, using questions already asked in the chat. Each
  section is a question with a title, a short why-this-question description,
  and an answer. Questions are grouped into categories with jump links. If
  the chat has no questions yet, ask the user and offer options instead of
  inventing the page. The HTML uses the calm internal-reference layout in
  template.html, including accordion cards, yellow highlights, comparison
  tables, and a light/dark toggle. Use when the user asks for a system
  description, project Q&A, how the system works, 問答, 系統說明, or to
  record project behavior in this format.
---

# Project Q&A

Write one `project-docs/QnA.html` file. Make sure `.gitignore` contains `project-docs/`.

Use questions already asked in this chat. If the chat has no questions yet, ask the user and offer options. Do not invent the page.

Each section is one question:

- A title.
- A short note on why this question matters.
- An answer.

Group questions into categories with jump links. On every update, group from the current questions:

- Reuse an existing category `id` and title when the topic fits.
- Add a category only when the file has none yet, or the topic does not match.

Align the UI with `.category-nav`, `a.jump`, `h2`, and `p.section-note`. Use the calm internal-reference layout in `template.html`: accordion cards, yellow highlights, comparison tables, and a light/dark toggle.

Example categories for a Traditional Chinese Q&A. These are examples, not a fixed set of four:

- `payslip-gen` — 產生糧單
- `setup-kmk` — Setup 與 KMK
- `local-dev` — 本機開發排錯
- `miniprogram` — HLD 小程序
