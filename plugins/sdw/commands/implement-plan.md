---
description: Implement an approved plan phase by phase. Run after create-plan.
---

# Implement Plan

Implement a reviewed and approved plan, phase by phase.

## Getting started

Read the plan path provided. If none was given, ask for one.

Read the plan completely. Note any existing checkmarks (`- [x]`) to understand what's already done. Then:

- Read all files the plan mentions
- Create a todo list to track progress
- Start with the first unchecked phase

## How to implement

**Follow the plan's intent, not just its words.** The plan was written before touching the code — reality may differ slightly. Use judgment and communicate clearly.

Work through one phase at a time:

1. Implement the changes for the phase
2. Run the test suite to verify the success criteria pass
3. Fix any failures before moving to the next phase
4. Check off completed items in the plan file

## When things don't match the plan

Stop and present it clearly before proceeding:

```
Issue in Phase [N]:
Expected: [what the plan says]
Found: [what's actually there]
Why it matters: [impact]

How should I proceed?
```

Don't work around mismatches silently. The plan was approved — deviations need approval too.

## Verification

After each phase, verify the success criteria pass. A phase isn't done until its criteria are met. Don't skip verification to save time — failures caught here are cheaper than failures caught in review.

## Resuming

If the plan has existing checkmarks, trust that completed work is done. Pick up from the first unchecked item. Only re-verify previous phases if something seems off.

**Next step**: After all phases complete → `/clear` → `/sdw:code-review`
