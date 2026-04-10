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

### Step by step

**1. Research** — understand what exists before building anything
```
/sdw:research-codebase
```
Tell Claude what you want to understand. It spawns parallel sub-agents to explore the codebase and outputs `research.md`. Then `/clear`.

**2. Plan** — create a detailed, phased implementation plan
```
/sdw:create-plan based on @.claude/ai/research-YYYY-MM-DD-topic.md
```
Interactive process. Claude researches, asks focused questions, proposes phases, writes `plan.md`. Then `/clear`.

**3. (Optional) Skeptic Gate**
```
Review this plan. Challenge it.
```
Claude adversarially reviews the plan. Fix weak spots before implementing. Then `/clear`.

**4. Implement** — execute the plan phase by phase
```
/sdw:implement-plan @.claude/ai/plan-YYYY-MM-DD-topic.md
```
Works through each phase, uses test-runner agent to verify, checks off tasks. Reset context between phases.

**5. Review** — catch issues before committing
```
/sdw:code-review
```
Runs tests via test-runner agent, checks for security issues, quality problems, test shortcuts. Outputs `review.md`.

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
| `/sdw:research-codebase` | Spawns parallel agents to research and outputs `research.md` |
| `/sdw:create-plan` | Interactive planning process, outputs `plan.md` |
| `/sdw:implement-plan` | Implements an approved plan phase by phase |
| `/sdw:code-review` | Reviews recent changes, runs tests, outputs `review.md` |
| `/sdw:research-prompt` | Transforms a "do X" prompt into a research-focused prompt |

---

## Customizing

The plugin gives you a base. To tweak a command or agent for your specific project:

1. Find the installed plugin at `~/.claude/plugins/cache/sdw*/`
2. Copy the file you want to modify to `.claude/commands/` or `.claude/agents/` in your project
3. Edit it freely — your standalone version is `/research-codebase` (no namespace), the plugin original stays at `/sdw:research-codebase`

Or for a full override:
```bash
cp -r ~/.claude/plugins/cache/sdw*/ ./my-sdw
# edit what you need
claude --plugin-dir ./my-sdw
```

> **Note**: Do not edit files in `~/.claude/plugins/cache/` directly. Changes there are wiped on `/plugin update`.

---

## Context Management Tips

- Use `/context` to check how much context is used
- Use `/clear` between phases to reset context
- Documents are saved to `.claude/ai/` — reference them with `@.claude/ai/filename.md`
- Spend most time on research and planning — problems there are cheap; problems in implementation are expensive
