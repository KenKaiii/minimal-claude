---
name: setup-commits
description: Generate a /commit command that runs checks, then commits with AI-generated messages
---

Generate a minimal `/commit` command that enforces quality checks before committing.

## Step 1: Detect Project and Extract Commands

Check for config files:
- `package.json` → Extract `lint`, `typecheck` scripts
- `pyproject.toml` → Use `mypy`, `pylint`
- `go.mod` → Use `go vet ./...`, `gofmt -l .`
- `Cargo.toml` → Use `cargo clippy`, `cargo fmt --check`

## Step 2: Generate /commit Command

Create `.claude/commands/commit.md`:

```markdown
---
name: commit
description: Run checks, commit with AI message, and push
---

1. Run quality checks:
   ```bash
   [PROJECT COMMANDS]
   ```
   Fix ALL errors before continuing.

2. Review changes: `git status` and `git diff`

3. Generate commit message:
   - Start with verb (Add/Update/Fix/Remove/Refactor)
   - Be specific and concise
   - One line preferred

4. Commit and push:
   ```bash
   git add -A
   git commit -m "your generated message"
   git push
   ```
```

**Keep it under 20 lines.**

## Step 3: Confirm

Tell user: ✅ `/commit` created. Quality checks + AI commits + auto-push enabled.
