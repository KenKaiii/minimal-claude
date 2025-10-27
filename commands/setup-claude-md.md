---
name: setup-claude-md
description: Generate a minimal CLAUDE.md with project-specific code quality guidelines
---

Generate a minimal CLAUDE.md file that enforces zero-tolerance code quality.

## Step 1: Detect Project Type

Check for config files to determine project type:
- `package.json` → JavaScript/TypeScript
- `pyproject.toml` or `requirements.txt` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust

Read the config file to find the exact linting and typechecking commands.

## Step 2: Extract Commands

**For JavaScript/TypeScript**: Check `package.json` scripts for `lint`, `typecheck`, `type-check`, or `tsc`, and check if there's a `dev` or `start` script (server)

**For Python**: Look for `mypy`, `pylint`, `black`, `ruff` in dependencies, and check for server commands (flask, fastapi, django)

**For Go**: Use `go vet ./...`, `gofmt -l .`, and check for `go run` server commands

**For Rust**: Use `cargo clippy`, `cargo fmt --check`, and check for `cargo run` server commands

## Step 3: Generate CLAUDE.md

Create `CLAUDE.md` in the project root with this EXACT format:

**If project has NO server:**
```markdown
# Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
[EXACT COMMANDS FROM PROJECT]
```

Fix ALL errors/warnings before continuing.
```

**If project HAS a server:**
```markdown
# Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
[EXACT COMMANDS FROM PROJECT]
```

Fix ALL errors/warnings before continuing.

If changes require server restart (not hot-reloadable):
1. Restart server
2. Read server output/logs
3. Fix ALL warnings/errors before continuing
```

**Keep it minimal (under 15 lines).**

### Examples:

**JavaScript/TypeScript (with server)**:
```markdown
# Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
npm run lint
npm run typecheck
```

Fix ALL errors/warnings before continuing.

If changes require server restart (not hot-reloadable):
1. Restart server
2. Read server output/logs
3. Fix ALL warnings/errors before continuing
```

**Python**:
```markdown
# Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
mypy .
pylint src/
```

Fix ALL errors/warnings before continuing.
```

**Go**:
```markdown
# Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
go vet ./...
gofmt -l .
```

Fix ALL errors/warnings before continuing.
```

**Rust**:
```markdown
# Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
cargo clippy
cargo fmt --check
```

Fix ALL errors/warnings before continuing.
```

## Step 4: Confirm

Tell the user:
- ✅ CLAUDE.md created
- 📋 Commands: [list them]
- 🎯 Zero-tolerance active

**Keep it minimal. No fluff. Just the essential enforcement.**
