---
name: setup-commits
description: Generate a /commit command that runs checks, then commits with AI-generated messages
---

Generate a `/commit` command that enforces code quality before committing.

## Step 1: Detect Project Type

Check for config files to determine project type:
- `package.json` → JavaScript/TypeScript
- `pyproject.toml` or `requirements.txt` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust

Read the config file to find the exact linting and typechecking commands.

## Step 2: Extract Commands

**For JavaScript/TypeScript**: Check `package.json` scripts for `lint`, `typecheck`, `type-check`, or `tsc`

**For Python**: Look for `mypy`, `pylint`, `black`, `ruff` in dependencies

**For Go**: Use `go vet ./...`, `gofmt -l .`

**For Rust**: Use `cargo clippy`, `cargo fmt --check`

## Step 3: Generate /commit Command

Create a file at `.claude/commands/commit.md` with this structure:

```markdown
---
name: commit
description: Run checks, then commit changes with AI-generated message
---

# Git Commit with Quality Checks

This command runs linting and typechecking, then creates a commit with a human-readable message.

## Step 1: Run Quality Checks

Run these commands:

[INSERT PROJECT-SPECIFIC COMMANDS]

If there are ANY errors or warnings:
1. Fix them immediately
2. Re-run checks
3. Only proceed when all checks pass

## Step 2: Review Changes

Run `git status` and `git diff --staged` (or stage files if needed) to see what's changed.

## Step 3: Generate Commit Message

Analyze the changes and create a clear, human-readable commit message:
- Start with a verb (Add, Update, Fix, Remove, Refactor, etc.)
- Be specific about what changed
- Keep it concise (one line preferred, max 2-3 lines)
- Focus on WHAT and WHY, not HOW

**Examples of good commit messages**:
- "Add user authentication with JWT tokens"
- "Fix memory leak in data processing loop"
- "Update API endpoints to use new response format"
- "Remove deprecated payment gateway integration"
- "Refactor database queries for better performance"

## Step 4: Commit and Push

1. Create the commit: `git commit -m "your message here"`
2. Push to remote: `git push`
3. Confirm completion to the user

**Important**:
- Never commit with errors/warnings
- Always generate meaningful commit messages
- Always push after committing (unless user specifies otherwise)
```

## Step 4: Customize Based on Project

**Replace `[INSERT PROJECT-SPECIFIC COMMANDS]` with actual commands.**

### For JavaScript/TypeScript:
```bash
npm run lint
npm run typecheck
```

### For Python:
```bash
mypy .
pylint src/
```

### For Go:
```bash
go vet ./...
gofmt -l .
```

### For Rust:
```bash
cargo clippy
cargo fmt --check
```

## Step 5: Confirm Completion

Tell the user:
- ✅ `/commit` command created at `.claude/commands/commit.md`
- 📋 Quality checks: [list commands]
- 💬 Commits will have AI-generated human-readable messages
- 🚀 Auto-push enabled after each commit

**Usage**: Run `/commit` to check code quality, create a smart commit, and push to remote.
