---
description: Research the codebase and produce research.md. Run this before planning anything.
---

# Research Codebase

Explore the codebase thoroughly to understand an area before building anything.

**Output**: Save findings to `.claude/ai/research-YYYY-MM-DD-topic.md`

## When invoked

Ask the user what they want to understand:

```
I'm ready to research the codebase. What would you like to understand?
```

Wait for their question, then explore.

## How to explore

Go broad first — find where things live, then go deep on what matters:

- Find all files related to the topic
- Understand how the relevant code works — trace data flow, key functions, patterns
- Find existing implementations that could inform the solution
- Note what conventions the codebase uses

Read files, search for symbols, grep for patterns. Prioritize concrete evidence over assumptions. Cite specific file paths and line numbers for every claim.

## Research document

Gather git metadata first (commit hash, branch, repo name), then save to `.claude/ai/research-YYYY-MM-DD-topic.md`:

```markdown
---
date: [ISO date with timezone]
git_commit: [current commit hash]
branch: [current branch]
repository: [repo name]
topic: "[research question]"
status: complete
---

# Research: [Topic]

**Date**: [date]
**Git Commit**: [hash]
**Branch**: [branch]

## Research Question

[Original question]

## Summary

[3-5 sentences answering the question directly]

## Findings

### [Area 1]
- [Finding — file:line]

### [Area 2]
- [Finding — file:line]

## Code References

- `path/to/file.py:123` — [what's there]

## Patterns & Conventions

[What conventions exist that future work should follow]

## Open Questions

[Anything that needs clarification before planning]
```

## After saving

Present a short summary of key findings. If there are open questions, surface them and wait for answers before finalizing the document.

**Next step**: Review research.md → `/clear` → `/sdw:create-plan`
