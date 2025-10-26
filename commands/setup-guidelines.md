---
name: setup-guidelines
description: Generate a minimal CLAUDE.md with project-specific code quality guidelines
---

You are creating a minimal CLAUDE.md file that enforces zero-tolerance code quality standards.

## Step 1: Detect Project Type and Tools

Check for these files to determine the project type and available tools:
- `package.json` → JavaScript/TypeScript (check scripts for lint, typecheck commands)
- `pyproject.toml` or `requirements.txt` → Python (check for mypy, pylint, black, ruff)
- `go.mod` → Go (go vet, gofmt, staticcheck)
- `Cargo.toml` → Rust (cargo clippy, cargo fmt)
- `composer.json` → PHP (phpcs, psalm)
- `build.gradle` or `pom.xml` → Java (checkstyle, spotbugs)

**Read the config file** to extract the exact commands used for:
- Linting
- Type checking
- Formatting

## Step 2: Generate CLAUDE.md

Create a file at `CLAUDE.md` in the project root with this structure:

```markdown
# Code Quality Guidelines

**Zero-tolerance policy**: All code must pass linting and type checking before completion.

## After Every Edit

After writing, editing, or updating ANY file, you MUST:

1. Run the following commands:
   [INSERT PROJECT-SPECIFIC COMMANDS]

2. Fix ALL errors and warnings immediately
3. Re-run checks until zero errors/warnings remain
4. Only then consider the task complete

## Commands

[INSERT SPECIFIC COMMANDS WITH EXAMPLES]

## Rules

- Never skip type checking or linting
- Never commit code with errors or warnings
- Fix issues immediately after they appear
- Run checks after EVERY file modification
```

### For JavaScript/TypeScript Projects

Extract commands from `package.json` scripts and generate:

```markdown
# Code Quality Guidelines

**Zero-tolerance policy**: All code must pass linting and type checking before completion.

## After Every Edit

After writing, editing, or updating ANY file, you MUST:

1. Run these commands:
   ```bash
   npm run lint          # or: yarn lint / pnpm lint
   npm run typecheck     # or: tsc --noEmit
   ```

2. Fix ALL errors and warnings immediately
3. Re-run checks until zero errors/warnings remain
4. Only then consider the task complete

## Commands

**Linting**: `npm run lint` or `eslint .`
**Type Checking**: `npm run typecheck` or `tsc --noEmit`
**Auto-fix**: `npm run lint -- --fix` (if available)

## Rules

- Never skip type checking or linting
- Never commit code with errors or warnings
- Fix issues immediately after they appear
- Run checks after EVERY file modification
```

### For Python Projects

```markdown
# Code Quality Guidelines

**Zero-tolerance policy**: All code must pass linting and type checking before completion.

## After Every Edit

After writing, editing, or updating ANY file, you MUST:

1. Run these commands:
   ```bash
   mypy .
   pylint src/
   black --check .
   ```

2. Fix ALL errors and warnings immediately
3. Re-run checks until zero errors/warnings remain
4. Only then consider the task complete

## Commands

**Type Checking**: `mypy .`
**Linting**: `pylint src/` or `ruff check .`
**Formatting**: `black .` or `ruff format .`

## Rules

- Never skip type checking or linting
- Never commit code with errors or warnings
- Fix issues immediately after they appear
- Run checks after EVERY file modification
```

### For Go Projects

```markdown
# Code Quality Guidelines

**Zero-tolerance policy**: All code must pass linting and type checking before completion.

## After Every Edit

After writing, editing, or updating ANY file, you MUST:

1. Run these commands:
   ```bash
   go vet ./...
   gofmt -l .
   staticcheck ./...
   ```

2. Fix ALL errors and warnings immediately
3. Re-run checks until zero errors/warnings remain
4. Only then consider the task complete

## Commands

**Vetting**: `go vet ./...`
**Formatting**: `gofmt -w .`
**Linting**: `staticcheck ./...`

## Rules

- Never skip type checking or linting
- Never commit code with errors or warnings
- Fix issues immediately after they appear
- Run checks after EVERY file modification
```

### For Rust Projects

```markdown
# Code Quality Guidelines

**Zero-tolerance policy**: All code must pass linting and type checking before completion.

## After Every Edit

After writing, editing, or updating ANY file, you MUST:

1. Run these commands:
   ```bash
   cargo clippy -- -D warnings
   cargo fmt -- --check
   cargo test
   ```

2. Fix ALL errors and warnings immediately
3. Re-run checks until zero errors/warnings remain
4. Only then consider the task complete

## Commands

**Linting**: `cargo clippy -- -D warnings`
**Formatting**: `cargo fmt`
**Type Checking**: `cargo check`

## Rules

- Never skip type checking or linting
- Never commit code with errors or warnings
- Fix issues immediately after they appear
- Run checks after EVERY file modification
```

## Step 3: Customize Based on Available Scripts

**Important**: Only include commands that actually exist in the project.

- For JS/TS: Check `package.json` scripts section for exact command names
- For Python: Check if tools are installed in dependencies
- For Go/Rust: Include standard toolchain commands

**Keep it minimal**: Only include the essential commands. No fluff.

## Step 4: Confirm Completion

After creating `CLAUDE.md`, inform the user:

1. ✅ CLAUDE.md created in project root
2. 📋 Commands included: [list the specific commands]
3. 🎯 Zero-tolerance policy active
4. 💡 This file will be automatically loaded in future Claude Code sessions

**Example output**:
```
✅ CLAUDE.md created successfully!

Commands configured:
  • npm run lint
  • npm run typecheck

Zero-tolerance policy is now active. After every file edit,
these commands will be run and all errors must be fixed immediately.
```

## Important Notes

- Keep CLAUDE.md under 100 lines
- Use exact commands from their project (don't invent new ones)
- Make it action-oriented, not explanatory
- Focus on the workflow: edit → check → fix → verify
- No boilerplate or fluff
