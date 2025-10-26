# Minimal Claude Code Plugin

A minimal base setup for creating Claude Code plugins with an intelligent `/setup` command that automatically configures project linting and typechecking.

## Structure

```
minimal-claude/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest (required)
├── commands/                # Slash commands
│   ├── setup-code-quality.md # Generate /fix command
│   ├── setup-claude-md.md    # Generate CLAUDE.md guidelines
│   ├── setup-commits.md      # Generate /commit command
│   └── example.md
├── agents/                  # Subagents
│   └── example-agent.md
├── skills/                  # Agent Skills
│   └── SKILL.md
└── hooks/                   # Event hooks
    └── hooks.json
```

## Featured Command: `/setup-code-quality`

The `/setup-code-quality` command intelligently detects your project type and configures automated code quality checks:

1. **Detects Project Type**: Automatically identifies if you're using JavaScript/TypeScript, Python, Go, Rust, PHP, or Java
2. **Checks Existing Tools**: Verifies which linting and typechecking tools are already installed
3. **Installs Missing Tools**: Only installs what's needed (eslint, prettier, mypy, clippy, etc.)
4. **Generates `/fix` Command**: Creates a custom `/fix` command tailored to your project that:
   - Runs all your linting and typechecking tools
   - Parses errors and groups them by domain (types, lint, formatting)
   - Spawns parallel agents to fix all issues simultaneously

### Usage

```bash
/setup-code-quality
```

After running setup, use the generated command:

```bash
/fix
```

This will automatically fix all linting and type errors in your project using parallel agents!

## Featured Command: `/setup-claude-md`

The `/setup-claude-md` command creates a minimal, non-bloated `CLAUDE.md` file with zero-tolerance code quality guidelines:

1. **Detects Project Type**: Identifies your project and its tooling
2. **Extracts Exact Commands**: Finds the actual lint/typecheck commands from your config
3. **Generates CLAUDE.md**: Creates a minimal guidelines file (under 100 lines) that:
   - Enforces running checks after EVERY file edit
   - Implements zero-tolerance for errors/warnings
   - Uses your project's specific commands
   - Gets automatically injected into Claude's prompt

### Usage

```bash
/setup-claude-md
```

This creates a `CLAUDE.md` file that tells Claude to automatically run your linting and typechecking commands after every edit, fixing all issues immediately.

**Example generated CLAUDE.md** (for a TypeScript project):
```markdown
# Code Quality Guidelines

**Zero-tolerance policy**: All code must pass linting and type checking.

## After Every Edit

After writing, editing, or updating ANY file, you MUST:

1. Run these commands:
   ```bash
   npm run lint
   npm run typecheck
   ```

2. Fix ALL errors and warnings immediately
3. Re-run checks until zero errors/warnings remain
```

**Minimal, actionable, effective.**

## Featured Command: `/setup-commits`

The `/setup-commits` command creates a `/commit` command that enforces quality checks before committing:

1. **Detects Project Type**: Identifies your project's linting/typechecking tools
2. **Runs Quality Checks**: Executes all checks before allowing commits
3. **Generates Smart Commit Messages**: AI-powered, human-readable commit messages
4. **Auto-push**: Automatically pushes to remote after committing

### Usage

```bash
/setup-commits
```

This creates a `/commit` command that:
1. Runs `npm run lint` and `npm run typecheck` (or your project's equivalent)
2. Only proceeds if all checks pass (zero tolerance)
3. Analyzes your changes
4. Generates a clear commit message like "Add user authentication with JWT"
5. Commits and pushes automatically

**Example workflow**:
```bash
# Make changes to your code
# Then run:
/commit

# Claude will:
# ✓ Run all quality checks
# ✓ Generate commit message
# ✓ Commit changes
# ✓ Push to remote
```

## Plugin Components

### Commands (`/commands`)
Custom slash commands that users can invoke. Each command is a Markdown file with frontmatter:

```markdown
---
description: Command description
---

Your command prompt here.
```

### Agents (`/agents`)
Specialized subagents that Claude can invoke for specific tasks. Define agents in Markdown files with frontmatter.

### Skills (`/skills`)
Agent Skills that Claude can invoke autonomously based on context. Skills are defined in `SKILL.md` files.

### Hooks (`/hooks`)
Event handlers that respond to Claude Code actions. Configure in `hooks.json`:

- `PostToolUse` - After any tool is used
- `UserPromptSubmit` - When user submits a prompt
- `SessionStart` - When a session starts

## Installation

### Option 1: Install from GitHub (Recommended)

Once you've pushed this to GitHub, users can install it directly:

```bash
# Add the marketplace
/plugin marketplace add your-username/minimal-claude

# Install the plugin
/plugin install minimal-claude@your-username
```

### Option 2: Local Testing

For local development and testing:

```bash
# Add local marketplace (from this directory)
/plugin marketplace add /Users/kenkai/Documents/UnstableMind/minimal-claude

# Install the plugin
/plugin install minimal-claude
```

### Option 3: Team Distribution

Add to your team's `.claude/settings.json`:

```json
{
  "pluginMarketplaces": [
    "your-username/minimal-claude"
  ],
  "plugins": [
    "minimal-claude@your-username"
  ]
}
```

This will auto-install the plugin for all team members who trust the repository.

## Publishing Your Plugin

### 1. Push to GitHub

```bash
git add -A
git commit -m "Initial commit: minimal-claude plugin with /setup command"
git branch -M main
git remote add origin https://github.com/your-username/minimal-claude.git
git push -u origin main
```

### 2. Share with Others

Users can now install your plugin with:

```bash
/plugin marketplace add your-username/minimal-claude
/plugin install minimal-claude@your-username
```

### 3. Update Plugin Version

When you make changes:

1. Update version in `.claude-plugin/plugin.json`
2. Update version in `.claude-plugin/marketplace.json`
3. Commit and push changes
4. Users will receive update notifications

## Customization

1. Edit `.claude-plugin/plugin.json` to update metadata
2. Add your custom commands in `commands/`
3. Add your custom agents in `agents/`
4. Add your skills in `skills/`
5. Configure your hooks in `hooks/hooks.json`

## Environment Variables

Use `${CLAUDE_PLUGIN_ROOT}` in paths to ensure portability across installations.
