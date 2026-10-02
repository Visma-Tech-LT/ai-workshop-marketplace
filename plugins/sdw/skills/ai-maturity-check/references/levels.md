<!-- Source: "AI Skill Maturity Level Evaluator" Gemini Gem by Agnius Paradnikas (Drive id 1BZKmZ98QWS_LwonwGN75zBbhTEYOg5xk) and the "AI Skill Maturity Levels" slides, Visma Tech Lithuania. Keep wording in sync with the source; do not reinterpret. -->

Five levels, two workflow types: Human-In-the-Loop (HITL, you approve actions) and Human-On-the-Loop (HOTL, "YOLO", you watch output). HOTL has no Level 1; Level 5 exists only as HOTL.

# AI Skill Maturity Levels

## Human-in-the-loop Levels

### Level 1: No AI / Minimal AI
You write code entirely by hand in your IDE, with occasional use of code completion. You may copy-paste from Google Gemini or similar tools, but AI is not part of your regular workflow.
* **Skills needed:** Prompting basics.

### Level 2: Coding Agent in IDE, Permissions On
You use a coding agent in IDE (e.g., Cursor, GitHub Copilot) that can run tools - but you approve each action manually before it executes. You stay in control of every step and review all changes carefully.  You're building trust and learning how the agent thinks. Review all changes accepting bigger changes as you build trust, but still you're copying local stack traces into a chat, re-explaining your project architecture for the third time, manually running tests after every change, switching between your ticket system and your editor dozens of times a day.
* **Skills needed:** How prompt pipeline is built (how prompt is formed by the tool?) and Token usage effectiveness.

### Level 3: Agent in CLI, Permissions On
You now run a broader, more capable agent from the CLI that handles larger, multi-step tasks but you still gate most of the actions. The scope of what the agent attempts has grown considerably, so approvals come more frequently and require real judgment to evaluate. By this level you have integrated your ticketing system, your agent takes care of running unit-tests or even deployment. You're essentially a careful reviewer of an increasingly capable co-worker.
* **Skills needed:** Creating and defining agents, Handling permissions, Context management, Knowledge about models, Comfortable with research/plan modes, Skills / hooks / commands, and Connecting needed tools (browser, etc.).

### Level 4: Multiple CLI Agents, Permissions On
You're managing several parallel agent instances simultaneously, but each still requires your approval to act. Coordination overhead is high - you're constantly context-switching between agents waiting on your Y/N. Productivity gains are real but limited by how fast you can review; this stage often pushes people to finally flip to YOLO.
* **Skills needed:** Uses backpressure (or similar approach) to drive agentic quality.
---

## Human-on-the-loop Levels (YOLO)

### Level 2: Agent in IDE, YOLO Mode
You've turned on YOLO mode and let the agent run more freely within your IDE. Trust has grown enough that you watch the output rather than gating each action. You're still anchored to the IDE environment, but your hands are less on the wheel. As the trust grows most of your IDE screen shows diffs and agent output rather than raw code. You interact with intent and direction, not individual lines; code review replaces code writing as your main activity.
* **Skills needed:** Same as human-in-the-loop Level 2 and Fluency in providing high-level directions and "intent" rather than line-by-line instructions.

### Level 3: CLI, Single Agent, YOLO
You've moved from the IDE to the terminal and run a single agent (e.g., Claude Code, Codex, Github Copilot CLI) in full autonomous mode. Diffs scroll by and you may or may not read all of them. You're operating significantly faster than before, with the agent handling entire tasks end-to-end.
* **Skills needed:** Same as human-in-the-loop Level 3 and CLI Environment Configuration: Mastering environment variables, tooling and local dependency management so agents can reliably run builds/tests, access various tools in a headless terminal environment.

### Level 4: CLI, Multiple Agents, YOLO
You routinely run 3-5 parallel agent instances simultaneously on different tasks or branches. You context-switch between agents rather than tasks, acting as a coordinator. Productivity is dramatically higher - you're starting to feel like a small team by yourself.
* **Skills needed:** Knowledge in setting up quality gates in each point of the process (linting, static security/dependency analysis, etc.) and Uses backpressure (or similar approach) to drive agentic quality and security.

### Level 5: Orchestrator
You've built or adopted tooling to orchestrate your fleet of agents programmatically (e.g., Gas Town, Claude Code Agent Team, etc.). Agents supervise other agents; you operate at the level of strategy and system design rather than task assignment. You're running a factory, not writing code nor reviewing it.
* **Skills needed:** Orchestration Patterns: Proficiency in designing non-linear workflows (Sequential, Parallel, and Routing) and Knowing when to use a "Router" agent versus a "Sub-agent" structure.
