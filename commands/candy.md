---
name: candy
description: Find low-risk, high-reward wins across the codebase using parallel exploration agents
---

Find quick wins in this codebase. Spawn 5 explore agents in parallel using the Task tool (subagent_type: Explore), each focusing on one area. Adapt each area to what's relevant for THIS project's stack and architecture.

**Agent 1 - Performance**: Inefficient algorithms, unnecessary work, missing early returns, blocking operations, things that scale poorly

**Agent 2 - Dead Weight**: Unused code, unreachable paths, stale comments/TODOs, obsolete files, imports to nowhere

**Agent 3 - Lurking Bugs**: Unhandled edge cases, missing error handling, resource leaks, race conditions, silent failures

**Agent 4 - Security**: Hardcoded secrets, injection risks, exposed sensitive data, overly permissive access, unsafe defaults

**Agent 5 - Dependencies & Config**: Unused packages, vulnerable dependencies, misconfigured settings, dead environment variables, orphaned config files

## The Only Valid Findings

A finding is ONLY valid if it falls into one of these categories:

1. **Dead** - Code that literally does nothing. Unused, unreachable, no-op.
2. **Broken** - Will cause errors, crashes, or wrong behavior. Not "might" - WILL.
3. **Dangerous** - Security holes, data exposure, resource exhaustion.

That's it. Three categories. If it doesn't fit, don't report it.

**NOT valid findings:**
- "This works but could be cleaner" - NO
- "Modern best practice suggests..." - NO
- "This is verbose/repetitive but functional" - NO
- "You could use X instead of Y" - NO
- "This isn't how I'd write it" - NO

If the code works, isn't dangerous, and does something - leave it alone.

## Output Format

For each finding:
```
[DEAD/BROKEN/DANGEROUS] file:line - What it is
Impact: What happens if left unfixed
```

Finding nothing is a valid outcome. Most codebases don't have easy wins - that's fine.
