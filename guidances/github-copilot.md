# Claude Code with Github Copilot as Model Provider

Guidance for how to connect [Github Copilot](https://github.com/features/copilot) as model provider for Claude Code.

> NOTICE: calling Github Copilot is not against its policy as this is officially supported per doc [here](https://docs.github.com/en/copilot/how-tos/build-copilot-extensions/building-a-copilot-agent-for-your-copilot-extension/using-copilots-llm-for-your-agent). And actually, there are lots of AI tools (e.g. Aider and Cline VSCode extension) already support Github Copilot as one of the LLM providers.

## 1) Install Claude Code and Copilot API proxy

```sh
npm install -g copilot-api @anthropic-ai/claude-code
```

## 2) Start copilot-api and authenticate to Github Copilot

```
$ copilot-api start
...
Please visit https://github.com/login/device and enter code XXXX-XXXX to authenticate
...
```

Once succeeds, you’d see the model list and API address:

```sh
...
- claude-3.5-sonnet
- claude-3.7-sonnet
- claude-3.7-sonnet-thought
- claude-sonnet-4
- claude-opus-4
- gemini-2.0-flash-001
- gemini-2.5-pro
- o3
...
  ➜ Listening on: http://localhost:4141/ (all interfaces)
```

## 3) Create Claude Code configure file `~/.claude/settings.json` with following contents

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://localhost:4141",
    "ANTHROPIC_AUTH_TOKEN": "dummy",
    "ANTHROPIC_MODEL": "claude-sonnet-4",
    "ANTHROPIC_SMALL_FAST_MODEL": "claude-3.7-sonnet",
    "DISABLE_NON_ESSENTIAL_MODEL_CALLS": "1",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1"
  }
}
```

## 4) Run claude

Open another terminal and then run `claude` at your will. DO read its [best practices](https://www.anthropic.com/engineering/claude-code-best-practices) for fully leveraging its capabilities.

## Alternative config

If the above configure file doesn't work, use env variable directly:

```sh
export ANTHROPIC_BASE_URL="http://localhost:4141"
export ANTHROPIC_AUTH_TOKEN="dummy"
export ANTHROPIC_MODEL="claude-sonnet-4"
export ANTHROPIC_SMALL_FAST_MODEL="claude-3.7-sonnet"
export DISABLE_NON_ESSENTIAL_MODEL_CALLS="1"
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC="1"

claude
```
