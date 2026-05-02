# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Korean-language documentation series — **"Claude Code 강의 실습용 환경 구축 가이드 시리즈"**. Each `.md` file at the repo root is a standalone tutorial in the series (install, API key setup, IDE integration, prompting, Skills, data analysis, etc.). There is **no application code, no build, no tests, no lint** — tasks here are almost always "write a new guide" or "edit an existing guide."

Two non-guide artifacts live alongside the guides as in-progress educational outputs from learners following the tutorials:

- `hello.py` — output of `first-conversation-hello-world.md`
- `python-calculator/` — output of `python-calculator-tutorial.md`

**Do not include these in commits unless explicitly asked.** They have been intentionally left staged/untracked across many sessions.

## Required structural template for every guide

All series guides share a strict template. New files must match it; otherwise they look out of place. Read any 2–3 existing guides (e.g. `status-reading-guide.md`, `effective-prompting-and-claude-md.md`) before writing a new one to absorb the rhythm.

Order is fixed:

1. `# Title with emoji`
2. `>` blockquote intro (one or two lines, evocative)
3. `## 🎯 학습 목표` — bulleted ✅ list
4. `## 📑 목차` — anchor links to every section
5. `## 📋 시작하기 전에` — prerequisites with cross-links to sibling guides (`./other-guide.md`)
6. Numbered sections: `## 1️⃣`, `## 2️⃣`, … (use the keycap-digit emojis, not plain numbers)
7. `## 🪞 5분 회고` — reflection questions + a `💭 토론거리` blockquote
8. `## 🆘 자주 막히는 지점` — Q&A FAQ
9. `## 🎯 오늘 배운 핵심 정리` — summary table + a 💎 takeaway blockquote
10. `## 📚 공식 문서` — only when there are real authoritative URLs to cite
11. `## 🎓 다음 단계` — next-step suggestions and links to other guides in the series
12. `## 🌱 마무리: Fail Forward` — three-color (🟢🟡🔴) reflection + a fenced learning-note template
13. Footer (mandatory, exact format):

```
📅 작성일: YYYY.MM.DD
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
```

Date uses dotted Korean format (`2026.05.02`), not ISO. The signature line is identical across every file.

## Voice and content conventions

- **Korean 존댓말** throughout (`~해요`, `~이에요`). Friendly, not formal/stiff.
- **Heavy use of comparison tables** — preferred over prose for any "X vs Y" or "when to use which" content.
- **Analogies for hard concepts** — Git as 택배, `/status` as 건강검진, CLAUDE.md as 입사 안내문, Skills as 요리 레시피. New analogies are welcome but commit to one and run with it.
- **Emoji indicators have semantic meaning**: ✅ do / ❌ don't / ⚠️ warning / 💡 tip / 🎯 goal / 🆘 help / 📚 docs / 🎓 next / 🌱 fail-forward / 🎬 scenario / 🏋️ exercise. Do not use emoji decoratively outside these slots.
- **OS variants use flag emojis**: 🍎 macOS, 🐧 Linux, 🪟 Windows.
- **Code blocks must declare language** (`bash`, `powershell`, `python`, `json`, `markdown`, `yaml`).
- **Cross-links between guides** use relative paths: `[제목](./filename.md)`.
- **"Fail Forward"** is the series' core pedagogical stance — failure is part of learning. Reinforce it in the closing section, never apologize for it.
- For Claude-Code-feature topics (Skills, Remote Control, MCP, hooks), **verify via the `claude-code-guide` agent or official docs before writing** — these features evolve and incorrect specifics get embarrassing fast. Mark uncertain claims explicitly rather than guessing.

## Filename conventions

Kebab-case is the norm (`api-key-setup.md`, `git-basics-easy.md`). A few legacy files use `claude_` prefix with an underscore (`claude_commands-reference.md`, `claude_interface-overview.md`). Don't normalize these silently — leave existing names alone unless the user asks. New files: kebab-case.

## Git workflow

The remote is `sinnarasam/claude-code-install-guide`. Direct pushes to `main` are blocked by branch protection — every change ships through a feature branch + PR.

- **Branch naming**: `add-<topic>` (matches the existing pattern: `add-status-reading-guide`, `add-claude-interface-overview`, etc.).
- **Commit message format**: `<filename>.md 추가` in Korean. Multi-line bodies are fine but keep the subject in this form.
- **Commit only the new file**, not unrelated staged changes (the `hello.py`/`python-calculator/` artifacts always linger). Use `git commit <path> -m "…"` rather than a bare `git commit`.
- **PR creation requires explicit user authorization** — `gh pr create` has been blocked when used proactively. After pushing the feature branch, surface the GitHub-provided PR-creation URL and let the user decide.
- Existing series PRs use the merge pattern `<filename>.md 추가 (#N)` once squash-merged.
