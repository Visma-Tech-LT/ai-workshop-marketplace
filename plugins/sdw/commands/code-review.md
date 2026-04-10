---
description: Review recent code changes for quality, security, and correctness. Run before committing.
---

# Code Review

Review recent code changes thoroughly before committing. Problems found here are free to fix — problems found after merging are not.

**Output**: Save to `.claude/ai/review-YYYY-MM-DD-topic.md`

## Review scope

Run `git diff` to see what changed. Focus on modified files and their immediate context.

## What to look for

**Security**
- No exposed secrets, API keys, or credentials in code or config
- Input is validated at system boundaries
- No obvious injection vulnerabilities

**Correctness**
- Logic does what it claims to do
- Edge cases are handled
- Errors are surfaced, not silently swallowed

**Test integrity** — zero tolerance
- No commented-out assertions
- No skip decorators added to avoid failures
- No test expectations weakened to match a wrong implementation
- If tests are failing and genuinely hard to fix, stop and explain why — don't paper over them

**Code quality**
- Code is clear enough for a teammate to understand without explanation
- No duplicated logic that could be consolidated
- New code follows existing patterns in the surrounding files

**Feature creep**
- Changes match what was planned — flag anything that wasn't requested

## Run the tests

Run the project's test suite and include results in the report:
- Pass / fail / skip counts
- Full error messages and stack traces for any failures

Don't skip this step.

## Review document

Gather git metadata first (commit hash, branch, repo name), then save to `.claude/ai/review-YYYY-MM-DD-topic.md`:

```markdown
---
date: [ISO date with timezone]
git_commit: [current commit hash]
branch: [current branch]
repository: [repo name]
status: complete
---

# Code Review: [Description]

**Date**: [date]
**Git Commit**: [hash]
**Branch**: [branch]
**Status**: Review Complete

## Summary

- **Overall**: ✅ APPROVED / ⚠️ APPROVED WITH CONDITIONS / ❌ REJECTED
- **Critical**: [N] issues — must fix before commit
- **Warnings**: [N] issues — should fix
- **Suggestions**: [N] items — optional

## Files Reviewed

[List of changed files]

## Test Results

✅ Passed: N | ⏭️ Skipped: N | ❌ Failed: N

[Full details for any failures]

## 🚨 Critical (Must Fix)

- **Issue**: [description — file:line]
- **Problem**: [what's wrong]
- **Fix**: [what to change]

## ⚠️ Warnings (Should Fix)

- **Issue**: [description — file:line]
- **Problem**: [concern]
- **Fix**: [recommendation]

## 💡 Suggestions (Optional)

- **Issue**: [description — file:line]
- **Benefit**: [improvement]
- **Approach**: [how]

## Approval

**Status**: [✅ APPROVED / ⚠️ APPROVED WITH CONDITIONS / ❌ REJECTED]

[Reasoning]
```

## After saving

Present the path and a short summary. Highlight any critical issues clearly.

If the review finds critical issues: fix them, then run `/sdw:code-review` again.
