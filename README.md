# Cursor custom skills

Personal [Cursor Agent Skills](https://cursor.com/docs) used across projects. Each folder contains a `SKILL.md` with YAML frontmatter and instructions for the agent.

## Install

Clone into your personal skills directory (Windows example):

```powershell
git clone https://github.com/Marcussyl/cursor-skills.git "$env:USERPROFILE\.cursor\skills-repo"
```

To use them as live skills, either:

- Copy or symlink each skill folder into `%USERPROFILE%\.cursor\skills\`, or
- Clone this repo directly to `%USERPROFILE%\.cursor\skills\` if that directory is only for these skills.

Do not put custom skills in `~/.cursor/skills-cursor/` — that path is reserved for Cursor built-in skills.

## Skills

| Skill | Summary |
|-------|---------|
| `answer-only` | Read and explain only; no file or git writes |
| `eli5` | Simple explanations (`/eli5 easy`, `chill`, `quick`) |
| `frontend-design` | Distinct UI direction; avoid generic AI layouts |
| `grilling` | Stress-test plans with numbered questions |
| `grill-me` | Explicit entry point for `grilling` |
| `project-qna` | Generate `project-docs/QnA.html` from chat Q&A |
| `task-observer` | Log patterns worth turning into new skills |
| `replay-briefly` | Short Chinese replies (`/replay-briefly`) |
| `commit-msg` | One-line conventional commit from staged files (`/commit-msg`) |

## Manual-invocation skills

These set `disable-model-invocation: true` and run only when you invoke them:

- `grill-me`
- `replay-briefly`
- `commit-msg`
