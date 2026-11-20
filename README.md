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

### Third-party skills (Jane Street)

Clone [janestreet/agent_skills](https://github.com/janestreet/agent_skills) next to this repo, then refresh vendored symlinks:

```bash
git clone https://github.com/janestreet/agent_skills.git ../agent_skills
# or: git -C ../agent_skills pull
```

Skills from that repo are symlinked into this tree (e.g. `socratic-tutor` → `../agent_skills/socratic-tutor`) so they load everywhere via `~/.cursor/skills`.

## Skills

| Skill | Summary |
|-------|---------|
| `answer-only` | Read and explain only; no file or git writes |
| `eli5` | Simple explanations (`/eli5 easy`, `chill`, `quick`) |
| `frontend-design` | Distinct UI direction; avoid generic AI layouts |
| `grilling` | Stress-test plans with numbered questions |
| `grill-me` | Explicit entry point for `grilling` |
| `project-qna` | Generate `project-docs/QnA.html` from chat Q&A |
| `html-critical-path-test-guide` | Critical-path code review + dark-theme HTML QA guide in `project-docs/` |
| `task-observer` | Log patterns worth turning into new skills |
| `replay-briefly` | Short Chinese, answer-only (`/replay-briefly`) |
| `reply-briefly-always` | Brief replies for the rest of the chat (`/reply-briefly-always`) |
| `commit-msg` | One-line conventional commit from staged files (`/commit-msg`) |
| `commit-batches` | Split work into related commits, then push (`/commit-batches`) |
| `socratic-tutor` | Socratic teaching sessions (`teach me`, `quiz me`, …) — vendored from [janestreet/agent_skills](https://github.com/janestreet/agent_skills) |

## Manual-invocation skills

These set `disable-model-invocation: true` and run only when you invoke them:

- `grill-me`
- `replay-briefly`
- `commit-msg`
- `commit-batches`
