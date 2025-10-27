---
name: setup-claude-md
description: Generate or update a minimal CLAUDE.md with project guidelines and structure
---

Generate or update a minimal CLAUDE.md with project structure, guidelines, and quality checks.

## Step 1: Check if CLAUDE.md Exists

If `CLAUDE.md` exists:
- Read the existing file
- Preserve custom sections the user may have added
- Update the structure, quality checks, and organization rules

If `CLAUDE.md` does NOT exist:
- Create a new one from scratch

## Step 2: Analyze Project (Use Explore Agents in Parallel)

Spawn parallel Explore agents to understand the codebase:

1. **Project Purpose Agent**: Analyze README, package.json description, main files to understand what the project does
2. **Directory Structure Agent**: Map out the folder structure and what each folder contains
3. **Tech Stack Agent**: Identify languages, frameworks, tools, dependencies

Wait for all agents to complete, then synthesize the information.

## Step 3: Detect Project Type & Commands

Check for config files:
- `package.json` → JavaScript/TypeScript (extract lint, typecheck, server scripts)
- `pyproject.toml` or `requirements.txt` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust

Extract:
- Linting commands
- Typechecking commands
- Server start command (if applicable)

## Step 4: Generate Project Tree

Create a concise tree structure showing key directories and files with brief descriptions.

Example format:
```
src/
  ├── api/          # API endpoints and routes
  ├── components/   # Reusable UI components
  ├── utils/        # Helper functions and utilities
  ├── types/        # TypeScript type definitions
  └── main.ts       # Application entry point
```

## Step 5: Generate or Update CLAUDE.md

Create `CLAUDE.md` with this structure:

```markdown
# [Project Name]

[Brief 1-2 sentence description of what this project does]

## Project Structure

[INSERT TREE HERE]

## Organization Rules

**Keep code organized and modularized:**
- API routes → `/api` folder, one file per route/resource
- Components → `/components`, one component per file
- Utilities → `/utils`, grouped by functionality
- Types/Interfaces → `/types` or co-located with usage
- Tests → Next to the code they test or in `/tests`

**Modularity principles:**
- Single responsibility per file
- Clear, descriptive file names
- Group related functionality together
- Avoid monolithic files

## Code Quality - Zero Tolerance

After editing ANY file, run:

```bash
[EXACT COMMANDS FROM PROJECT]
```

Fix ALL errors/warnings before continuing.

[IF SERVER EXISTS:]
If changes require server restart (not hot-reloadable):
1. Restart server: `[SERVER COMMAND]`
2. Read server output/logs
3. Fix ALL warnings/errors before continuing
```

**Keep total file under 100 lines.**

## Step 6: Preserve Custom Sections

If updating an existing CLAUDE.md:
- Keep any custom sections the user added
- Update the generated sections (Project Structure, Quality Checks)
- Merge carefully without losing user content

## Step 7: Confirm Completion

Tell the user:
- ✅ CLAUDE.md [created/updated]
- 📋 Project: [brief description]
- 🗂️ Structure mapped with [X] directories
- 📐 Organization rules enforced
- 🎯 Zero-tolerance quality checks active
