# Minimal Claude Code Plugin

A minimal base setup for creating Claude Code plugins with an intelligent `/setup` command that automatically configures project linting and typechecking.

## Structure

```
minimal-claude/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest (required)
├── commands/                # Slash commands
│   ├── setup.md            # Smart project setup command
│   └── example.md
├── agents/                  # Subagents
│   └── example-agent.md
├── skills/                  # Agent Skills
│   └── SKILL.md
└── hooks/                   # Event hooks
    └── hooks.json
```

## Featured Command: `/setup`

The `/setup` command intelligently detects your project type and configures automated code quality checks:

1. **Detects Project Type**: Automatically identifies if you're using JavaScript/TypeScript, Python, Go, Rust, PHP, or Java
2. **Checks Existing Tools**: Verifies which linting and typechecking tools are already installed
3. **Installs Missing Tools**: Only installs what's needed (eslint, prettier, mypy, clippy, etc.)
4. **Generates `/check` Command**: Creates a custom `/check` command tailored to your project that:
   - Runs all your linting and typechecking tools
   - Parses errors and groups them by domain (types, lint, formatting)
   - Spawns parallel agents to fix all issues simultaneously

### Usage

```bash
/setup
```

After running setup, use the generated command:

```bash
/check
```

This will automatically fix all linting and type errors in your project using parallel agents!

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
