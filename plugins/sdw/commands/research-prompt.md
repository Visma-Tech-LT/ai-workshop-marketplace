---
description: 
---

# Research Prompt Transformer

You are tasked with transforming user prompts into research-focused prompts optimized for codebase exploration. Users often express what they want to *do* (implement, add, fix, change), but effective codebase research requires understanding what *exists* first.

## Input

The user's original prompt: $ARGUMENTS

## Your Task

Analyze the provided prompt and transform it into a research-focused prompt that:

1. **Focuses on current state** - What exists today? How does it work?
2. **Identifies patterns and conventions** - What approaches are already used?
3. **Removes solution bias** - No assumptions about how to solve the problem
4. **Seeks concrete references** - Guides toward specific files, locations, and examples
5. **Explores connections** - Cross-component relationships and dependencies
6. **Finds usage patterns** - How things are actually used, not just where they're defined

## Analysis Process

### Step 1: Identify Intent Categories

Classify elements of the original prompt into:

- **Research-appropriate**: Questions about current state, patterns, architecture, behavior
- **Solution-oriented**: Implementation details, specific approaches, "add X", "change Y to Z"
- **Assumption-laden**: Presumes how something works or should work without verification

### Step 2: Extract Core Research Questions

For each solution-oriented element, derive the underlying research questions:

| Solution Intent | Research Questions |
|-----------------|-------------------|
| "Add authentication" | How is auth currently handled? What auth patterns exist? Where are protected routes? |
| "Fix the bug in X" | How does X work? What's the data flow? What's expected vs actual behavior? |
| "Refactor Y to use Z" | How is Y structured? Where is Z used elsewhere? What would be affected? |
| "Improve performance of X" | How does X currently perform? What's the execution path? Where are bottlenecks? |
| "Add a button to..." | Where is this UI? What's the component structure? What similar interactions exist? |

### Step 3: Generate Research Prompt

Create a research prompt that:

- Starts with understanding, not doing
- Asks questions that lead to concrete file locations and code examples
- Explores how similar problems are solved elsewhere in the codebase
- Considers what components interact with the area of interest
- Looks for existing patterns that could inform the eventual solution

## Output Format

Respond with exactly this structure:

---

## Research Prompt

[The transformed, research-focused prompt - 3-8 sentences that guide thorough codebase exploration without implementation bias]

---

## Transformation Notes

### Removed/Transformed Elements

| Original Element | Why Removed/Changed | Research Alternative |
|------------------|--------------------|--------------------|
| [specific text from original] | [explanation] | [what to investigate instead] |

### Preserved Elements

- [List elements that were already research-appropriate and kept as-is]

### Key Areas to Explore

1. [Specific component or area to investigate]
2. [Patterns or conventions to identify]
3. [Relationships or dependencies to understand]
4. [Examples or similar implementations to find]

---

## Examples

**Example 1:**

Original: "Add a dark mode toggle to the settings page"

Research Prompt: "How is theming currently implemented in this codebase? Where is the settings page located and what is its component structure? Are there existing toggle components or UI patterns for feature switches? How do other features handle user preferences and persistence?"

**Example 2:**

Original: "Fix the authentication bug where users get logged out randomly"

Research Prompt: "How does the authentication system work? What manages session state and token lifecycle? Where is logout triggered and what conditions cause it? What logging or error handling exists around auth state changes?"

**Example 3:**

Original: "Refactor the API layer to use GraphQL instead of REST"

Research Prompt: "How is the current API layer structured? What endpoints exist and what patterns do they follow? How is data fetching handled on the client side? Are there any existing GraphQL implementations or related dependencies in the codebase?"

**Example 4:**

Original: "Implement a webhook system to notify external services when tasks complete"

Research Prompt: "How are external integrations currently handled? What event systems or notification mechanisms exist? Where and how are task status changes detected? Are there existing patterns for outbound HTTP requests or callbacks? How is configuration for external services stored?"

---

Now analyze the provided prompt and generate the research-focused version.
