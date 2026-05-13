---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git diff:*), Bash(git rm:*), Bash(git ls-files:*), Bash(find:*), Bash(ls:*), Bash(cat:*), Write
argument-hint: [message]
description: Create a git commit with context
---

## Context

- Current git status: !`git status`
- Current git diff: !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

## Your task

### Step 1 — Ensure a .gitignore exists and is correct

Check whether `.gitignore` exists: !`ls .gitignore 2>/dev/null || echo MISSING`

If it is MISSING:
1. Detect the project type by inspecting files present (e.g. `pyproject.toml`/`requirements.txt` → Python, `package.json` → Node.js, `go.mod` → Go, `Cargo.toml` → Rust, `*.gemspec`/`Gemfile` → Ruby).
2. Create `.gitignore` with entries appropriate for that stack. Always include these baseline entries:
   - Python: `__pycache__/`, `*.pyc`, `.venv/`, `venv/`, `dist/`, `*.egg-info/`, `.env`
   - Node.js: `node_modules/`, `dist/`, `.env`, `*.log`
   - Go: the binary name (from `go.mod`), `*.test`
   - Generic: `.DS_Store`, `*.swp`
3. Stage the new `.gitignore` with `git add .gitignore`.

If `.gitignore` already exists, read it and check whether obvious project-specific patterns are missing (e.g. `__pycache__/` for a Python project). If anything important is absent, append it and re-stage the file.

### Step 2 — Remove already-tracked files that should be ignored

Run: !`git ls-files --cached --ignored --exclude-standard`

If any files appear, remove them from the index with `git rm --cached <file>` (one at a time, not with `-r` unless it's a directory you're certain about). This does not delete the files on disk — it just stops tracking them.

### Step 3 — Commit

Based on all staged changes, group them into one commit (or multiple if the changes are clearly unrelated).

If a message was provided via arguments, use it: $ARGUMENTS

Otherwise, use conventional commits format:
- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation changes
- `refactor:` for code refactoring
- `test:` for adding tests
- `chore:` for maintenance tasks

---
**Last Updated**: May 7, 2026


