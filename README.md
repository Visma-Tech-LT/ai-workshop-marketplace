# AI Engineering Workshop — Plugin Marketplace

Plugin marketplace for the **AI Engineering Workshop, Part 2: Spec-Driven Workflow**.

## Install

```shell
/plugin marketplace add github:Visma-Tech-LT/ai-workshop-marketplace
/plugin install sdw@ai-workshop
```

That's it. You now have 6 agents and 5 workflow commands available.

---

## The Workflow

```
/sdw:research-codebase   →   /sdw:create-plan   →   /sdw:implement-plan   →   /sdw:code-review
```

Run each command, review its output, then proceed to the next. This is intentional — explained below.

### Step by step

**1. Research** — understand what exists before building anything
```
/sdw:research-codebase
```
Tell Claude what you want to understand. It explores the codebase and outputs `research.md`. Review it, then `/clear`.

**2. Plan** — create a detailed, phased implementation plan
```
/sdw:create-plan based on @.claude/ai/research-YYYY-MM-DD-topic.md
```
Interactive process. Claude asks questions, proposes phases, writes `plan.md`. Review it, then `/clear`.

**3. (Optional) Skeptic Gate**
```
Review this plan. Challenge it.
```
Claude adversarially reviews the plan. Fix weak spots before implementing. Then `/clear`.

**4. Implement** — execute the plan phase by phase
```
/sdw:implement-plan @.claude/ai/plan-YYYY-MM-DD-topic.md
```
Works through each phase, runs tests to verify, checks off tasks. Reset context between phases.

**5. Review** — catch issues before committing
```
/sdw:code-review
```
Runs tests, checks for security issues, quality problems, test shortcuts. Outputs `review.md`.

---

## Why it's manual and sequential

You might wonder: why not run the whole thing automatically in one command?

**The pauses are the lesson.** At each step you have to look at what Claude produced and make a conscious decision:

- After research: *Does this capture what I need to know? Did it miss anything?*
- After planning: *Is this actually what I want to build? Is the scope right?*
- After implementing: *Did it follow the plan? Does the review show anything I need to fix?*

Those decisions are the habit this workflow is building. If you skip them, you're not using spec-driven development — you're just generating code faster and hoping it's right.

**Mistakes in research compound.** If research misses something important and you go straight to implementation, Claude will build the wrong thing confidently. The human checkpoint between each phase exists to catch drift before it becomes expensive.

**Context is a resource, not a given.** The `/clear` between phases isn't just housekeeping — it's a forcing function. It makes the document the handoff, not the conversation. `research.md` is what carries knowledge from phase 1 into phase 2. `plan.md` carries it from phase 2 into phase 3. The documents are the contract.

**The workflow only works if you engage with the outputs.** Run the command, read the document, decide to proceed. That's the loop. Once that habit is internalized, you can move faster — but speed comes after the mental model is built, not before.

---

## Agents

| Agent | Purpose |
|---|---|
| `codebase-locator` | Finds WHERE code lives — files, directories, entry points |
| `codebase-analyzer` | Explains HOW code works — data flow, logic, patterns |
| `codebase-pattern-finder` | Shows existing patterns with code examples to model after |
| `test-runner` | Discovers and runs the test suite, reports full error details |
| `code-reviewer` | Senior code review with zero tolerance for test shortcuts |
| `web-search-researcher` | Researches web sources for answers to technical questions |

Claude invokes these automatically. You don't call them directly.

---

## Commands

| Command | What it does |
|---|---|
| `/sdw:research-codebase` | Explores the codebase and outputs `research.md` |
| `/sdw:create-plan` | Interactive planning process, outputs `plan.md` |
| `/sdw:implement-plan` | Implements an approved plan phase by phase |
| `/sdw:code-review` | Reviews recent changes, runs tests, outputs `review.md` |
| `/sdw:research-prompt` | Transforms a "do X" prompt into a research-focused prompt |

---

## Context Management Tips

- Use `/context` to check how much context is used
- Use `/clear` between phases to reset context
- Documents are saved to `.claude/ai/` — reference them with `@.claude/ai/filename.md`
- Spend most time on research and planning — problems there are cheap; problems in implementation are expensive

---

## Customizing

The plugin gives you a base. To tweak a command or agent for your specific project:

1. Find the installed plugin at `~/.claude/plugins/cache/sdw*/`
2. Copy the file you want to modify to `.claude/commands/` or `.claude/agents/` in your project
3. Edit it freely — your standalone version is `/research-codebase` (no namespace), the plugin original stays at `/sdw:research-codebase`

> **Note**: Do not edit files in `~/.claude/plugins/cache/` directly. Changes there are wiped on `/plugin update`.
