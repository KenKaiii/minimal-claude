---
name: setup-updates
description: Generate a /update-app command for dependency updates and deprecation fixes
---

Generate a minimal `/update-app` command that updates dependencies and fixes deprecations.

## Step 1: Detect Project Type

Check for config files:
- `package.json` → JavaScript/TypeScript (npm/yarn/pnpm/bun)
- `pyproject.toml` or `requirements.txt` → Python (pip/poetry)
- `go.mod` → Go
- `Cargo.toml` → Rust
- `composer.json` → PHP

## Step 2: Detect Package Manager

**For JavaScript/TypeScript**: Check for lock files:
- `package-lock.json` → npm
- `yarn.lock` → yarn
- `pnpm-lock.yaml` → pnpm
- `bun.lockb` → bun

**For Python**: Check for:
- `poetry.lock` → poetry
- Otherwise → pip

## Step 3: Generate /update-app Command

Create `.claude/commands/update-app.md`:

```markdown
---
name: update-app
description: Update dependencies, fix deprecations and warnings
---

# Dependency Update & Deprecation Fix

## Step 1: Check for Updates

[INSERT CHECK COMMAND]

## Step 2: Update Dependencies

[INSERT UPDATE COMMAND]

## Step 3: Check for Deprecations & Warnings

Run installation and check output:
[INSERT INSTALL COMMAND]

Read ALL output carefully. Look for:
- Deprecation warnings
- Security vulnerabilities
- Peer dependency warnings
- Breaking changes

## Step 4: Fix Issues

For each warning/deprecation:
1. Research the recommended replacement or fix
2. Update code/dependencies accordingly
3. Re-run installation
4. Verify no warnings remain

## Step 5: Run Quality Checks

[INSERT QUALITY CHECK COMMANDS]

Fix all errors before completing.

## Step 6: Verify Clean Install

Ensure a fresh install works:
1. Delete dependency folders/caches
2. Run clean install
3. Verify ZERO warnings/errors
4. Confirm all dependencies resolve correctly
```

## Step 4: Customize by Project Type

**Replace placeholders with actual commands:**

### JavaScript/TypeScript (npm):
```markdown
## Step 1: Check for Updates
```bash
npm outdated
```

## Step 2: Update Dependencies
```bash
npm update
npm audit fix
```

## Step 3: Check for Deprecations & Warnings
```bash
rm -rf node_modules package-lock.json
npm install
```

## Step 5: Run Quality Checks
```bash
npm run lint
npm run typecheck
```

## Step 6: Verify Clean Install
```bash
rm -rf node_modules package-lock.json
npm install
```
```

### JavaScript/TypeScript (yarn):
```markdown
## Step 1: Check for Updates
```bash
yarn outdated
```

## Step 2: Update Dependencies
```bash
yarn upgrade
yarn audit
```

## Step 3: Check for Deprecations & Warnings
```bash
rm -rf node_modules yarn.lock
yarn install
```
```

### Python (pip):
```markdown
## Step 1: Check for Updates
```bash
pip list --outdated
```

## Step 2: Update Dependencies
```bash
pip install --upgrade -r requirements.txt
```

## Step 3: Check for Deprecations & Warnings
```bash
pip install -r requirements.txt
```

## Step 5: Run Quality Checks
```bash
mypy .
pylint src/
```
```

### Python (poetry):
```markdown
## Step 1: Check for Updates
```bash
poetry show --outdated
```

## Step 2: Update Dependencies
```bash
poetry update
```

## Step 3: Check for Deprecations & Warnings
```bash
poetry install
```
```

### Go:
```markdown
## Step 1: Check for Updates
```bash
go list -u -m all
```

## Step 2: Update Dependencies
```bash
go get -u ./...
go mod tidy
```

## Step 3: Check for Deprecations & Warnings
```bash
go mod download
```

## Step 5: Run Quality Checks
```bash
go vet ./...
gofmt -l .
```
```

### Rust:
```markdown
## Step 1: Check for Updates
```bash
cargo outdated
```

## Step 2: Update Dependencies
```bash
cargo update
```

## Step 3: Check for Deprecations & Warnings
```bash
cargo check
```

## Step 5: Run Quality Checks
```bash
cargo clippy
cargo fmt --check
```
```

## Step 5: Confirm Completion

Tell the user:
- ✅ `/update-app` created
- 🔄 Updates: [package manager commands]
- ⚠️ Zero-tolerance for deprecations/warnings
- 🛡️ Security audit included
- ✨ Clean install verification enabled
