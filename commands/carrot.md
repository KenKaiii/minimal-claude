---
name: carrot
description: Verify implementations against real-world code samples and official documentation using parallel agents
---

Verify this codebase against current best practices and official documentation. Spawn 8 explore agents in parallel using the Task tool (subagent_type: Explore), each focusing on one category. Each agent must VERIFY findings using Grep MCP (real code samples) or WebSearch (official docs) - no assumptions allowed.

**Agent 1 - Core Framework**: Detect the main framework (React, Next, Express, Django, Rails, etc.), verify usage patterns against official documentation via WebSearch

**Agent 2 - Dependencies/Libraries**: Check if library APIs being used are current or deprecated. Verify against library documentation and Grep MCP for how modern codebases use these libraries

**Agent 3 - Language Patterns**: Identify the primary language (TypeScript, Python, Go, etc.), verify idioms and patterns are current. Use Grep MCP to see how modern projects write similar code

**Agent 4 - Configuration**: Examine build tools, bundlers, linters, and config files. Verify settings against current tool documentation via WebSearch

**Agent 5 - Security Patterns**: Review auth, data handling, secrets management. Verify against current security guidance and OWASP recommendations via WebSearch

**Agent 6 - Testing**: Identify test framework in use, verify testing patterns match current library recommendations. Check via docs and Grep MCP for modern test patterns

**Agent 7 - API/Data Handling**: Review data fetching, state management, storage patterns. Verify against current patterns via Grep MCP and framework docs

**Agent 8 - Error Handling**: Examine error handling patterns, verify they match library documentation. Use Grep MCP to compare against real-world implementations

## Agent Workflow

Each agent MUST follow this process:
1. **Identify** - What's relevant in THIS project for your category
2. **Find** - Locate specific implementations in the codebase
3. **Verify** - Check against Grep MCP (real code) OR WebSearch (official docs)
4. **Report** - Only report when verified current practice differs from codebase

## The Only Valid Findings

A finding is ONLY valid if:
1. **OUTDATED** - Works but uses old patterns with verified better alternatives
2. **DEPRECATED** - Uses APIs marked deprecated in current official docs
3. **INCORRECT** - Implementation contradicts official documentation

**NOT valid findings:**
- "I think there's a better way" without verification - NO
- "This looks old" without proof - NO
- Style preferences or subjective improvements - NO
- Anything not verified via Grep MCP or official docs - NO

## Output Format

For each finding:
```
[OUTDATED/DEPRECATED/INCORRECT] file:line - What it is
Current: How it's implemented now
Verified: What the correct/current approach is
Source: Grep MCP (X repos) | URL to official docs
```

No findings is a valid outcome. If implementations match current practices, that's good news.
