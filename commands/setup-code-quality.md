---
name: setup-code-quality
description: Detect project tools and generate a /check command for linting and typechecking
---

You are setting up a project for automated code quality checks. Follow these steps carefully:

## Step 1: Detect Project Type

Check for these files in the current directory to determine the project type:
- `package.json` → JavaScript/TypeScript (Node.js)
- `pyproject.toml` or `requirements.txt` or `setup.py` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust
- `composer.json` → PHP
- `build.gradle` or `pom.xml` → Java

Read the relevant config file to understand the project structure.

## Step 2: Check Existing Tools

Based on the project type, check if these tools are already configured:

### JavaScript/TypeScript:
- Check `package.json` for: `eslint`, `prettier`, `typescript`, `@typescript-eslint/*`
- Check for config files: `.eslintrc.*`, `.prettierrc.*`, `tsconfig.json`
- Check `package.json` scripts for: `lint`, `typecheck`, `type-check`, or `tsc`

### Python:
- Check for: `mypy`, `pylint`, `black`, `ruff`, `flake8` in dependencies
- Check for config files: `mypy.ini`, `.pylintrc`, `pyproject.toml`
- Look for linting/type checking configurations

### Go:
- Check for: `golint`, `gofmt`, `staticcheck`
- Go has built-in tools, check if project uses them

### Rust:
- Check for: `clippy`, `rustfmt` (built-in to Rust toolchain)
- Check `Cargo.toml` for workspace configuration

## Step 3: Install Missing Tools (if needed)

If tools are missing, install them based on the project type:

### JavaScript/TypeScript:
```bash
# Detect package manager (npm, yarn, pnpm, bun)
# Install missing tools, e.g.:
npm install --save-dev eslint prettier typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin

# Add scripts to package.json if missing:
# "lint": "eslint ."
# "typecheck": "tsc --noEmit"
```

### Python:
```bash
pip install mypy pylint black ruff
# or add to requirements-dev.txt / pyproject.toml
```

### Go:
```bash
go install golang.org/x/lint/golint@latest
go install honnef.co/go/tools/cmd/staticcheck@latest
```

### Rust:
```bash
rustup component add clippy rustfmt
```

**IMPORTANT**: Always check if tools exist first. Only install if missing.

## Step 4: Generate /fix Command

Create a file at `.claude/commands/fix.md` with the following structure:

```markdown
---
name: fix
description: Run typechecking and linting, then spawn parallel agents to fix all issues
---

# Project Code Quality Check

This command runs all linting and typechecking tools for this project, collects errors, groups them by domain, and spawns parallel agents to fix them.

## Step 1: Run Linting and Typechecking

Run the appropriate commands for this project:

[INSERT PROJECT-SPECIFIC COMMANDS HERE]

## Step 2: Collect and Parse Errors

Parse the output from the linting and typechecking commands. Group errors by domain:
- **Type errors**: Issues from TypeScript, mypy, etc.
- **Lint errors**: Issues from eslint, pylint, ruff, clippy, etc.
- **Format errors**: Issues from prettier, black, rustfmt, gofmt

Create a list of all files with issues and the specific problems in each file.

## Step 3: Spawn Parallel Agents

For each domain that has issues, spawn an agent in parallel using the Task tool:

**IMPORTANT**: Use a SINGLE response with MULTIPLE Task tool calls to run agents in parallel.

Example:
- Spawn a "type-fixer" agent for type errors
- Spawn a "lint-fixer" agent for lint errors
- Spawn a "format-fixer" agent for formatting errors

Each agent should:
1. Receive the list of files and specific errors in their domain
2. Fix all errors in their domain
3. Run the relevant check command to verify fixes
4. Report completion

## Step 4: Verify All Fixes

After all agents complete, run the full check again to ensure all issues are resolved.
```

**Replace `[INSERT PROJECT-SPECIFIC COMMANDS HERE]` with the actual commands for the detected project type.**

### JavaScript/TypeScript Example:
```bash
npm run lint
npm run typecheck
```

### Python Example:
```bash
mypy .
pylint src/
black --check .
```

### Go Example:
```bash
go vet ./...
staticcheck ./...
gofmt -l .
```

### Rust Example:
```bash
cargo clippy -- -D warnings
cargo fmt -- --check
```

## Step 5: Confirm Completion

After generating the `/fix` command, inform the user:
1. What project type was detected
2. Which tools were already present
3. Which tools were installed (if any)
4. That the `/fix` command has been created at `.claude/commands/fix.md`
5. How to use it: "Run `/fix` to lint, typecheck, and auto-fix all issues"

**Important Notes**:
- Always create the `.claude/commands/` directory if it doesn't exist
- Ensure the YAML frontmatter includes both `name` and `description`
- The generated `/fix` command must spawn agents in parallel (single response, multiple Task tool calls)
- Tailor the commands to what's actually available in the project
