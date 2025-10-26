# Installation Instructions

## Quick Install

```bash
# Add the marketplace
/plugin marketplace add KenKaiii/minimal-claude

# Install the plugin
/plugin install minimal-claude@KenKaiii
```

## What You Get

After installation, you'll have access to the `/setup` command:

```bash
/setup
```

This command will:
1. Detect your project type (JS/TS, Python, Go, Rust, PHP, Java)
2. Check which linting and typechecking tools are already installed
3. Install any missing tools (if needed)
4. Generate a custom `/check` command for your project

Then use the generated command:

```bash
/check
```

This will:
1. Run all your linting and typechecking tools
2. Parse errors and group them by domain (types, lint, formatting)
3. Spawn parallel agents to fix all issues simultaneously

## Supported Project Types

- **JavaScript/TypeScript**: eslint, prettier, typescript
- **Python**: mypy, pylint, black, ruff
- **Go**: golint, gofmt, staticcheck
- **Rust**: clippy, rustfmt
- **PHP**: phpcs, psalm
- **Java**: checkstyle, spotbugs

## Requirements

- Claude Code (latest version)
- Git repository for your project
- Package manager for your language (npm/yarn/pnpm, pip, cargo, etc.)

## Troubleshooting

### Plugin not found
```bash
# Remove and re-add marketplace
/plugin marketplace remove KenKaiii
/plugin marketplace add KenKaiii/minimal-claude
/plugin install minimal-claude@KenKaiii
```

### Command not available
- Restart Claude Code after installation
- Check plugin is installed: `/plugin list`

### /setup not detecting project
- Ensure you have a config file (package.json, pyproject.toml, etc.) in your directory
- Run from the root of your project

## Uninstall

```bash
/plugin uninstall minimal-claude
/plugin marketplace remove KenKaiii
```

## Support

- GitHub Issues: https://github.com/KenKaiii/minimal-claude/issues
- Repository: https://github.com/KenKaiii/minimal-claude
