# Using Claude Code with AI-VERDE

Claude Code is Anthropic's official CLI coding assistant. AI-VERDE can serve as the backend for Claude Code, routing requests through AI-VERDE's budget controls and guardrails to Anthropic Claude models hosted on AWS Bedrock.

!!! Note

    Unlike the [non-Bedrock Claude Code setup](api-key-claude.md), which uses `ANTHROPIC_API_KEY`, the Bedrock setup must put your AI-VERDE API key in `ANTHROPIC_AUTH_TOKEN`. When talking to a Bedrock endpoint, Claude Code only sends `ANTHROPIC_AUTH_TOKEN`; an `ANTHROPIC_API_KEY` would be ignored.

## Prerequisites

1. Obtain your **AI-VERDE API key** and note the **AI-VERDE base URL**. The base URL used in the environment variables ends in `/bedrock` rather than `/v1`. [Instructions can be found here](api-key.md).
2. Note the **Claude model ID** for Opus, Sonnet, and Haiku. [Instructions for listing available models can be found here](api-key-models.md). Model names in AI-VERDE are prefixed with an identifier for your course or team, separated by a dash or a slash (e.g. `my-team-claude-sonnet-4-6` or `my-team/claude-sonnet-4-6`).
3. Install **Claude Code**. Instructions can be found at [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup).
4. The remaining instructions assume you have an open terminal with Claude Code installed on Linux or macOS.

## 1. Configure Claude Code

### Option 1: `~/.claude/settings.json` (recommended)

Add the following `env` section to `~/.claude/settings.json` (create the file if it does not exist). Settings in this file apply every time you run Claude Code, in any terminal.

```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "<your-ai-verde-api-key>",
    "ANTHROPIC_BEDROCK_BASE_URL": "https://llm-api.cyverse.ai/bedrock",
    "CLAUDE_CODE_SKIP_BEDROCK_AUTH": "1",
    "CLAUDE_CODE_USE_BEDROCK": "1",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "<model name for opus>",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "<model name for sonnet>",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "<model name for haiku>"
  }
}
```

For example:

```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "sk-xxxxxxxxxxxxxxxxxxxxxx",
    "ANTHROPIC_BEDROCK_BASE_URL": "https://llm-api.cyverse.ai/bedrock",
    "CLAUDE_CODE_SKIP_BEDROCK_AUTH": "1",
    "CLAUDE_CODE_USE_BEDROCK": "1",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "my-team-claude-opus-4-6",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "my-team-claude-sonnet-4-6",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "my-team-claude-haiku-4-5"
  }
}
```

If the file already has other settings, add the `env` section alongside them rather than replacing the file.

### Option 2: Shell environment variables

Alternatively, export the same variables in your terminal before launching Claude Code:

```bash
export ANTHROPIC_AUTH_TOKEN="<your-ai-verde-api-key>"
export ANTHROPIC_BEDROCK_BASE_URL=https://llm-api.cyverse.ai/bedrock
export CLAUDE_CODE_SKIP_BEDROCK_AUTH=1
export CLAUDE_CODE_USE_BEDROCK=1
export ANTHROPIC_DEFAULT_OPUS_MODEL="<model name for opus>"
export ANTHROPIC_DEFAULT_SONNET_MODEL="<model name for sonnet>"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="<model name for haiku>"
```

Exported variables only last for the current terminal session. To avoid re-entering them each session, add the lines to your shell profile (e.g. `~/.bashrc` or `~/.zshrc`), then source your shell profile.

!!! Note

    To obtain the AI-VERDE Bedrock Base URL, simply substitute `/v1` with `/bedrock`, e.g. `https://llm-api.cyverse.ai/v1` to `https://llm-api.cyverse.ai/bedrock`. If both `~/.claude/settings.json` and your shell set the same variable, the value in `~/.claude/settings.json` is used.

## 2. Launch Claude Code

Start Claude Code:

```bash
claude
```

You can run `/status` inside Claude Code to confirm it is using Amazon Bedrock with the AI-VERDE base URL.

## If you need to change your API Key

If for some reason you need to change your VERDE API Key, update `ANTHROPIC_AUTH_TOKEN` wherever you set it in step 1 (`~/.claude/settings.json` or your shell profile), then restart Claude Code.
