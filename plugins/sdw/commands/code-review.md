---
description: 
---

# Code Review

Use the code-reviewer agent to conduct a comprehensive review of all recent code changes. The agent will examine the code for security vulnerabilities, code quality issues, performance problems, testing coverage, and compatibility concerns.

The code-reviewer agent will provide specific, actionable feedback with code examples and prioritize critical issues that could affect security, functionality, or maintainability.

**Output**: Review report will be saved to `.claude/ai/review-YYYY-MM-DD-description.md`

## Steps to follow:

1. **Gather metadata for the review report:**
   - Gather relevant metadata from git (commit hash, branch name, repository name, timestamps)
   - Filename: `.claude/ai/review-YYYY-MM-DD-description.md`
     - Format: `review-YYYY-MM-DD-description.md` where:
       - YYYY-MM-DD is today's date
       - description is a brief kebab-case description
     - Examples:
       - `review-2025-10-03-feature-implementation.md`
       - `review-2025-10-03-bug-fixes.md`

2. **Use the code-reviewer agent with metadata:**
   - Pass the metadata to the code-reviewer agent for structured report generation
   - The agent will examine code for security vulnerabilities, quality issues, performance problems, testing coverage, and compatibility concerns
   - Agent will generate a review report with proper frontmatter and metadata

3. **Review report structure:**
   - The agent will create a comprehensive report with metadata followed by content:

     ```markdown
     ---
     date: [Current date and time with timezone in ISO format]
     reviewer: Claude
     git_commit: [Current commit hash]
     branch: [Current branch name]
     repository: [Current repository name]
     review_type: "code-review"
     tags: [code-review, quality-assurance, security]
     status: complete
     last_updated: [Current date in YYYY-MM-DD format]
     last_updated_by: Claude
     related_plan: "[Path to related plan document if available, e.g., .claude/ai/plan-2025-10-01-complete-validation-coverage.md]"
     related_research: "[Path to related research document if available, e.g., .claude/ai/research-2025-10-01-validation-status.md]"
     # Code Review Report: [Issue Title/Description]

     **Date**: [Current date and time with timezone]
     **Reviewer**: Claude Code Reviewer
     **Git Commit**: [Current commit hash]
     **Branch**: [Current branch name]
     **Repository**: [Repository name]
     **Status**: Review Complete

     ## Related Documents

     - **Plan**: [Link to plan document if available]
     - **Research**: [Link to research document if available]
     
     ## Review Summary

     - **Overall Status**: ✅ APPROVED / ⚠️ APPROVED WITH CONDITIONS / ❌ REJECTED
     - **Critical Issues**: X found (must fix before commit)
     - **Warnings**: X found (should address)
     - **Suggestions**: X found (optional improvements)

     ## Changes Reviewed

     [List of files and changes reviewed]

     ## Critical Issues

     [Issues that must be fixed]

     ## Warnings

     [Issues that should be addressed]

     ## Suggestions

     [Optional improvements]

     ## Security Analysis

     [Security-specific findings]

     ## Performance Considerations

     [Performance-related findings]

     ## Test Coverage

     [Testing-related findings]

     [Rest of the review content...]
     ```

4. **Save and present review completion:**
   - Save the review report to `.claude/ai/review-YYYY-MM-DD-description.md`
   - Present a concise summary of the review findings to the user
   - Include the path to the generated review report
   - Highlight any critical issues that require immediate attention

The code-reviewer agent will provide specific, actionable feedback with code examples and prioritize critical issues that could affect security, functionality, or maintainability.

## Important Notes:

- Always run fresh git analysis - the review should reflect the current state of changes
- The review report should be self-contained with all necessary context
- Include temporal context (when the review was conducted) via metadata
- Focus on finding concrete security issues, quality problems, and maintainability concerns
- Provide specific file paths and line numbers for developer reference
- Ensure all metadata fields are properly populated using git commands