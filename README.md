### .claude Workspace

This repository is your local workspace for automations, agents, commands, and configuration used with Claude/Cursor on macOS.

It contains reusable prompts, task runners, and project logs to speed up day‑to‑day development.

## Quick start

- Clone/sync this folder to `~/.claude` (already set up on this machine).
- Open it in Cursor to browse agents, commands, and configs.
- Customize `settings.json` and `plugins/config.json` as needed.

## Directory layout

- `agents/`: Role presets and multi-step planners
  - `fullstack-developer.md`: End‑to‑end feature work
  - `tech-lead-planner.md`: High‑level plans and risk analysis
  - `feature-analyzer.md`: Scope/impact analysis
  - `code-reverter.md`: Safe revert strategies
- `commands/`: One‑shot utilities you can trigger
  - `commit.md`: Conventional commit helper
  - `refactor-test.md`: Refactor with test guidance
- `guidances/`: Integration and gateway settings
  - `litellm_config.yaml`, `llm-gateway-litellm.md`
- `plugins/`: Plugin definitions and cached repo data
  - `config.json`: Enable/disable plugins and set options
  - `repos/`: Plugin state/cache
- `projects/`: Session logs per project (jsonl transcripts)
- `ide/`: Internal IDE session locks
- `statsig/`: Feature flag/session telemetry cache
- `todos/`: Persisted task lists per session
- `CLAUDE.md`: Short notes on workspace intent
- `settings.json`: User/workspace preferences

## Recommended environment

- macOS with zsh (default here)
- Python available as `python3`/`pip3` if needed by tools

## Usage patterns

### Agents
- Open an agent file in `agents/` and start a session using it as a system prompt.
- Tweak role wording to match your project; keep tool-specific details in the agent file.

### Commands
- Use files in `commands/` to standardize repetitive tasks (e.g., commits, refactors).
- Copy/edit to add your own command playbooks.

### Plugins
- Configure plugin behavior in `plugins/config.json`.
- Keep secrets out of the repo; use environment variables instead.

### Project transcripts
- Each subdirectory in `projects/` mirrors a local project and stores `.jsonl` session logs for traceability.
- Safe to prune older logs if space is a concern.

## Customization tips

- Prefer editing existing agents/commands over creating many near-duplicates.
- Store sensitive tokens outside this repo; reference via env vars.
- Keep prompts concise; link out to docs instead of inlining large texts.

## Troubleshooting

- Workspace not recognized: ensure the directory is `~/.claude` and readable.
- Plugin errors: validate `plugins/config.json` is valid JSON and required env vars are set.
- Conflicting sessions: remove stale locks in `ide/*.lock` if a previous run crashed.

## Conventions

- Keep commit messages conventional (feat, fix, docs, chore).
- Prefer small, composable agents/commands with clear responsibilities.
