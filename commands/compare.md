---
name: compare
description: Compare code you just created against real-world code samples via Grep MCP to verify best practices and completeness
---

Compare the code you just created or modified in this conversation against real-world implementations using the `mcp__grep__searchGitHub` tool.

You already know what you just built. For each file you created or modified, use `mcp__grep__searchGitHub` to search for how real projects implement the same patterns. Look at the specific APIs, hooks, functions, and architecture you used.

If you find something consistently done differently across real codebases, or something commonly included that you left out, report it:

```
[MISSING/DIVERGENT/INCOMPLETE] file:line - What it is
Wrote: What was implemented
Real-world: What real projects do instead/additionally
Evidence: Grep MCP - pattern seen in X out of Y repos searched
```

Style preferences and subjective improvements are not valid findings. Only report things backed by clear Grep MCP evidence across multiple repos.

If the code aligns well with real-world patterns, say so. That's a good outcome.
