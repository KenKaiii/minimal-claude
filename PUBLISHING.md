# Publishing Guide

This guide will help you publish the minimal-claude plugin so others can use it.

## Quick Publish Checklist

- [ ] Update `.claude-plugin/plugin.json` with your details
- [ ] Update `.claude-plugin/marketplace.json` with your contact info
- [ ] Create GitHub repository
- [ ] Push code to GitHub
- [ ] Share installation instructions

## Step-by-Step Publishing

### 1. Update Plugin Metadata

Edit `.claude-plugin/plugin.json`:

```json
{
  "name": "minimal-claude",
  "description": "Intelligent project setup that auto-configures linting, typechecking, and parallel agent-based fixing",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  }
}
```

### 2. Update Marketplace Info

Edit `.claude-plugin/marketplace.json`:

```json
{
  "name": "minimal-claude-marketplace",
  "owner": {
    "name": "Your Name",
    "email": "your-email@example.com"
  },
  "plugins": [
    {
      "name": "minimal-claude",
      "description": "Intelligent project setup that auto-configures linting, typechecking, and parallel agent-based fixing",
      "version": "1.0.0",
      "author": {
        "name": "Your Name"
      },
      "source": "."
    }
  ]
}
```

### 3. Initialize Git and Create Repository

```bash
# Already initialized locally
git add -A
git commit -m "Initial commit: minimal-claude plugin with /setup command"

# Create repository on GitHub (via web or gh CLI)
gh repo create minimal-claude --public --source=. --remote=origin

# Or manually:
# 1. Go to https://github.com/new
# 2. Create repository named "minimal-claude"
# 3. Then run:
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/minimal-claude.git
git push -u origin main
```

### 4. Share Installation Instructions

Users can now install your plugin:

```bash
# Add your marketplace
/plugin marketplace add YOUR-USERNAME/minimal-claude

# Install the plugin
/plugin install minimal-claude@YOUR-USERNAME
```

### 5. Test Installation

Test that your plugin installs correctly:

```bash
# Remove if previously installed
/plugin uninstall minimal-claude

# Add marketplace
/plugin marketplace add YOUR-USERNAME/minimal-claude

# Install plugin
/plugin install minimal-claude@YOUR-USERNAME

# Restart Claude Code
# Test the command
/setup
```

## Updating Your Plugin

When you make changes:

1. **Update version numbers**:
   - `.claude-plugin/plugin.json` → bump version
   - `.claude-plugin/marketplace.json` → bump version

2. **Commit and push**:
   ```bash
   git add -A
   git commit -m "v1.1.0: Add new feature"
   git tag v1.1.0
   git push origin main --tags
   ```

3. **Users update**:
   ```bash
   /plugin update minimal-claude
   ```

## Distribution Options

### Option A: Public GitHub Repository
- Most common and easiest
- Users install with: `/plugin marketplace add username/repo`

### Option B: Private Repository
- For team/organization use
- Requires authentication
- Users need repository access

### Option C: Local Marketplace
- For development/testing
- Add with full path: `/plugin marketplace add /path/to/plugin`

## Marketplace Submission

To get featured on community marketplaces:

1. **claudecodemarketplace.com** - Submit via their contribution process
2. **Community GitHub repos** - Create PR to add your plugin
3. **Anthropic's official channels** - Check for submission guidelines

## Support

- Documentation: https://docs.claude.com/en/docs/claude-code/plugins
- Community: GitHub Discussions or relevant forums
- Issues: Enable GitHub Issues for bug reports

---

**Ready to publish?** Follow the steps above and share your plugin with the Claude Code community!
