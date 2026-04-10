---
description: Create an implementation plan interactively. Run after research, before implementing.
---

# Create Plan

Create a detailed, phased implementation plan through an interactive process. Be skeptical and thorough — problems found in planning are cheap. Problems found in implementation are expensive.

**Output**: Save to `.claude/ai/plan-YYYY-MM-DD-topic.md`

## When invoked

If a research document was provided, read it fully first. Then ask:

```
I'll help you create an implementation plan. Based on [the research / what you've described],
I understand we need to [summary].

Before I start planning, I have a few questions:
- [question you couldn't answer from existing context]
- [question about scope or constraints]
```

If nothing was provided:

```
I'll help you create an implementation plan. Please share:
- What you want to build or change
- Any research documents (e.g. @.claude/ai/research-*.md)
- Constraints or requirements I should know about
```

## Planning process

Work collaboratively — get agreement at each step, not all at once:

1. **Understand the codebase** — read files relevant to the task before proposing anything. Only ask questions you genuinely can't answer by reading the code.

2. **Propose structure first** — outline phases before writing details. Get agreement before expanding.

3. **Write the full plan** — once structure is agreed, write a complete, actionable plan.

4. **Iterate** — refine until the user is satisfied. No open questions should remain in the final plan.

## What makes a good plan

- **Phases are incremental** — each phase produces something testable
- **Success criteria are specific** — each checkbox is either done or not done, no ambiguity
- **Scope is explicit** — include a "What we're NOT doing" section to prevent creep
- **Grounded in actual code** — reference real file paths and line numbers, not abstractions

## Plan document

Gather git metadata first (commit hash, branch, repo name), then save to `.claude/ai/plan-YYYY-MM-DD-topic.md`:

```markdown
---
date: [ISO date with timezone]
git_commit: [current commit hash]
branch: [current branch]
repository: [repo name]
topic: "[feature or task name]"
status: complete
---

# [Feature] Implementation Plan

**Date**: [date]
**Git Commit**: [hash]
**Branch**: [branch]

## Overview

[What we're building and why — 2-3 sentences]

## Current State

[What exists today, what's missing, key constraints discovered]

## What We're NOT Doing

[Explicit scope boundary — prevents scope creep]

## Phase 1: [Name]

### Changes

**File**: `path/to/file.ext`
[What changes and why]

### Success Criteria

- [ ] [Specific, verifiable outcome]
- [ ] [Another outcome]

---

## Phase 2: [Name]

[Same structure...]

## Testing Strategy

[How to verify the full implementation works end to end]
```

## After saving

Present the plan path and ask:
- Are the phases properly scoped?
- Are the success criteria specific enough?
- Anything missing?

Iterate until the user is satisfied.

**Next step**: Review plan.md → optionally challenge it → `/clear` → `/sdw:implement-plan`
