# AGENTS.md: superpowers (fork exhuman777/superpowersex)

Instructions for an AI agent working on this repo (standard https://agents.md). Human docs: `README.md`, history: `CHANGELOG.md`, `RELEASE-NOTES.md`.

## What this is
A skills library and workflow (brainstorm → plan → subagent-driven TDD → review) shipped as a plugin for several agents: Claude Code (`.claude-plugin/`), Cursor (`.cursor-plugin/`), Codex (`.codex/INSTALL.md`), OpenCode (`.opencode/`), Gemini CLI (`gemini-extension.json` + `GEMINI.md`).

## Layout
- `skills/<name>/SKILL.md`: one skill per folder (frontmatter `name`, `description`), supporting files next to it.
- `agents/`: subagent definitions. `commands/`: slash commands. `hooks/`: session hooks.
- `GEMINI.md`: context file for Gemini extension users (imports `using-superpowers`). It is product content, not instructions for you.
- `tests/`: shell and node tests per platform.

## Tests
- Brainstorm server: `cd tests/brainstorm-server && npm install && npm test`.
- Claude Code skills (needs `claude` CLI and the plugin installed locally): `tests/claude-code/run-skill-tests.sh` (fast), `--integration` (slow, 10-30 min).
- Skill triggering: `tests/skill-triggering/run-all.sh`. Explicit requests: `tests/explicit-skill-requests/run-all.sh`. OpenCode: `tests/opencode/run-tests.sh`.
- Run the tests that cover what you changed before committing.

## Writing and changing skills
- Follow `skills/writing-skills/SKILL.md` (TDD for documentation: watch an agent fail without the skill, then write it).
- Skills must stay agent-agnostic: refer to project instructions as `AGENTS.md` (with `CLAUDE.md` / `GEMINI.md` as fallbacks), tool names per platform in `skills/using-superpowers/references/`.
- On release: bump `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` (other manifests follow upstream) and add a `CHANGELOG.md` entry.

## Commits and PRs
Small focused commits, imperative subject. Upstream is `obra/superpowers`: keep fork-only changes easy to rebase.
