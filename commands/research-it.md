---
name: research-it
description: Research the best 2026 tools, deps, and patterns for what you want to build, then output a concise RESEARCH.md
---

Research the best tools, dependencies, and architecture for the user's project. The user will describe what they want to build. If no description is provided, analyze the current codebase to infer the project type and goals.

First, ask the user: **"What are you building? Describe features, target platform, and any constraints."** (Skip if they already provided this with the command.)

Store the user's description as `$PROJECT_DESC`.

Then spawn **6 agents in parallel** using the Agent tool (subagent_type: Explore). Every agent receives `$PROJECT_DESC` and must verify ALL recommendations using WebSearch or Grep MCP (mcp__grep__searchGitHub) - no training-data assumptions allowed.

**Agent 1 - Project Scan**: Read the current working directory. Catalog what already exists: package.json, config files, installed deps, directory structure, language/framework already chosen. Report exactly what's in place so other agents don't duplicate it.

**Agent 2 - Stack Validation**: Given `$PROJECT_DESC` and what Agent 1 would find in a typical scaffold, research via WebSearch whether the current framework/language is the best choice for this project in 2026. Compare top 2-3 alternatives on performance, ecosystem, and developer experience. Pick ONE winner. If the current stack is already the best choice, confirm it with evidence.

**Agent 3 - Core Dependencies**: For EACH feature in `$PROJECT_DESC`, find the single best library for this stack in 2026. Use WebSearch to confirm latest stable version numbers. Use Grep MCP to verify real projects actually use these libraries. No outdated packages. No "popular in 2023" picks. Output: package name, exact latest version, one-line purpose.

**Agent 4 - Dev Tooling**: Research the best 2026 dev tooling for this stack: package manager, bundler, linter, formatter, test framework, type checker. Use WebSearch to verify current recommendations. Pick ONE per category. Include exact versions.

**Agent 5 - Architecture**: Use Grep MCP to find how real 2026 projects of this type structure their code. Look for directory layouts, file naming conventions, and key patterns (state management, routing, data fetching, etc.). Output a concrete directory tree and list of patterns to follow.

**Agent 6 - Config & Integration**: Research required config files for the chosen stack and tools. Use WebSearch for current config best practices. Cover: linter config, formatter config, TS/type config, env setup, CI/CD basics, deployment target config. Provide exact file contents or key settings.

## Agent Rules

1. Every recommendation MUST be verified via WebSearch or Grep MCP - no guessing
2. Confirm 2026 latest stable versions - do not assume version numbers from training data
3. Pick ONE best option per category - no "you could also use X"
4. No prose, no hedging, no alternatives lists - decisive answers only
5. If something already exists in the project scaffold, note it and don't re-recommend it unless it should be replaced

## Output

After all agents complete, synthesize their findings into a single `RESEARCH.md` file written to the project root. The file must be optimized for LLM consumption - zero fluff, maximum actionability. Use this exact structure:

```markdown
# RESEARCH: [short project description]
Generated: [today's date]
Stack: [framework + language + runtime]

## INSTALL
[exact shell commands to run - copy-paste ready, in order]

## DEPENDENCIES
| package | version | purpose |
|---------|---------|---------|
[each purpose max 5 words]

## DEV DEPENDENCIES
| package | version | purpose |
|---------|---------|---------|
[each purpose max 5 words]

## CONFIG FILES TO CREATE
### [filename]
[exact file contents or key settings]
[repeat for each config file]

## PROJECT STRUCTURE
[tree showing recommended directories and key files]

## SETUP STEPS
1. [concrete action]
2. [concrete action]
[ordered, each step is one command or action]

## KEY PATTERNS
[brief list of architectural patterns to follow, with one-line descriptions]

## SOURCES
[URLs used for verification, grouped by section]
```

Rules for RESEARCH.md:
- No alternatives sections
- No explanations of "why" - just what to do
- No "you could also use X" hedging
- Every version number must be verified, not assumed
- Commands must be copy-paste ready
- The entire file should be readable by another LLM session that can immediately execute the setup

Write the file using the Write tool, then tell the user it's ready and summarize what was researched.
