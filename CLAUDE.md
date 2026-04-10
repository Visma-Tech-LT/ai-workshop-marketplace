# CLAUDE.md

Plugin marketplace for AI Engineering Workshop Part 2.

## Command design

Commands in `plugins/sdw/commands/` are playbook-style — they describe
what good output looks like for each workflow phase, not how to orchestrate
agents to produce it. Do not add explicit agent-spawning instructions to commands.
Agents are invoked automatically based on their descriptions.

## Versioning

Version bumps are automated via GitHub Actions on every push to main.
Do not manually edit `version` fields in plugin.json or marketplace.json.

## Workflow philosophy

The research → plan → implement → review sequence is intentionally manual
and sequential. Do not create a command that chains phases automatically.
The human review between each phase is the point.
