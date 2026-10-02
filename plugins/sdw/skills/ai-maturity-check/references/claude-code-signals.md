# Claude Code signals per level

Baseline: Claude Code **2.1.287**, written 2026-10-02. Anything released after this
version is not in this table — the changelog check in SKILL.md step 3 covers it.

The rubric is tool-agnostic. This table says what each rubric skill looks like as
observable Claude Code evidence. A signal supports a level; it never proves one
on its own. Weigh what the person actually did (report, session data) over what
is merely installed (config).

## Workflow type: HITL vs HOTL

| Evidence | Points to |
|---|---|
| `permissions.defaultMode` is `default`/`manual` or `plan`; few `allow` rules | HITL |
| No `defaultMode` set anywhere (interactive sessions then start in auto mode) | HOTL, unless the report shows the person switching back to manual |
| `defaultMode` is `acceptEdits` (edits run unasked, shell still gated) | HITL, moving toward HOTL |
| `defaultMode` is `auto` (a classifier approves actions instead of you) | HOTL |
| `defaultMode` is `bypassPermissions` | HOTL |
| `skipDangerousModePermissionPrompt: true` (only hides the bypass-mode warning) | Weak HOTL hint; never decisive on its own |
| `auto`/`bypassPermissions` set only in project `.claude/settings*.json` | Ignored by Claude Code — does not count |
| Broad `allow` rules (e.g. `Bash(*)`, whole tool families) | HOTL |
| Report: long autonomous stretches, few interruptions, "let it run" patterns | HOTL |
| Report: frequent short replies, approvals, corrections mid-task | HITL |

Config shows today's default only — insights session data does not record the
permission mode per session. When config and report disagree, say so and let
the report win for the past period.

## Level evidence

| Level | Rubric skill | Claude Code evidence |
|---|---|---|
| 2 | Prompt pipeline, token effectiveness | Uses `/context`, `/compact`, `/clear` deliberately; `CLAUDE.md` kept short |
| 3 | Creating and defining agents | Custom subagents in `~/.claude/agents/` or `.claude/agents/`; `Agent`/`Task` tool in Top Tools |
| 3 | Handling permissions | Curated `allow`/`deny` rules; sandbox settings |
| 3 | Context management | Subagents used to keep the main context clean; `/compact` with instructions |
| 3 | Knowledge about models | Deliberate model per task (`/model`, `opusplan`, per-agent `model:` frontmatter, `/advisor`) |
| 3 | Research / plan modes | Plan mode, spec-first skills (e.g. `sdw` research → plan) |
| 3 | Skills / hooks / commands | Own skills, hooks in settings, installed plugins |
| 3 | Connecting needed tools | MCP servers (ticketing, browser, docs); `uses_mcp` in session data |
| 3 | Ticketing integrated, agent runs tests/deploys | Jira/GitHub MCP or `gh` in Bash; test/build commands run by Claude |
| 3 HOTL | CLI environment configuration | Agent runs builds/tests headless without help; `env` in settings; `claude -p` usage |
| 4 | Several parallel agents | Report "Multi-Clauding (Parallel Sessions)"; git worktrees; background agents (`claude agents`) |
| 4 | Backpressure / quality gates | Hooks that block on lint/test/security; reviewer agents run after implementation; Stop hooks that gate completion |
| 5 | Programmatic orchestration | Workflow tool scripts, agent teams / teammates, routines (`/schedule`), `/loop`, Agent SDK or headless pipelines where agents supervise agents |
| 5 | Router vs sub-agent design | Own orchestrator skills/agents that route work to specialised agents and gate their output |

## Insights data available locally

- `~/.claude/usage-data/report.html` — the latest `/insights` report (dated copies sit beside it).
  Sections: What You Work On, What You Wanted, Top Tools Used, Languages, Session Types,
  How You Use Claude Code, User Response Time Distribution, Multi-Clauding (Parallel Sessions),
  User Messages by Time of Day, Tool Errors Encountered, Impressive Things You Did,
  What Helped Most, Outcomes, Primary Friction Types, Inferred Satisfaction,
  Existing CC Features to Try, Suggested CLAUDE.md Additions, New Ways to Use Claude Code, On the Horizon.
- `~/.claude/usage-data/session-meta/*.json` — per session: `tool_counts`, `uses_task_agent`,
  `uses_mcp`, `user_interruptions`, `user_response_times`, `git_commits`, `duration_minutes`, …
- `~/.claude/usage-data/facets/*.json` — per session: `session_type`, `outcome`, `friction_counts`, …

If a later Claude Code version renames these sections or fields, trust what the files contain
and note the drift in the output.
