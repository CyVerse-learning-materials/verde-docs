# Claude Code (using Anthropic Models)

You can follow these instructions to use your VERDE API Key after installing Claude Code. More information on using Claude Code can be found here, [https://code.claude.com/docs/en/overview](https://code.claude.com/docs/en/overview).

!!! Note

    These instructions assume you are using a space that is connected to Anthropic models (Fable/Opus/Sonnet/Haiku from Anthropic, Azure or other providers with Anthropic-style APIs). If you need access to Claude Code using a non-Anthropic model, then see the [instructions here](api-key-claude-non-anthropic.md) or use [Claude Code Router](claude-code-router.md).

!!! Note

    If your model is hosted on AWS Bedrock, then see the [instructions here](aws_bedrock_claude_code.md). The Bedrock setup uses `ANTHROPIC_AUTH_TOKEN` instead of `ANTHROPIC_API_KEY`, because Claude Code only sends `ANTHROPIC_AUTH_TOKEN` when talking to a Bedrock endpoint.

## Prerequisites

1. Your VERDE course or team must be configured to use Anthropic models (see instructor or team lead).
2. Obtain your VERDE API Key. [Instructions can be found here](api-token.md).
3. Note the model names for the Opus, Sonnet, and Haiku models available to your course or team. [Instructions for listing available models can be found here](api-key-models.md).
4. Install Claude Code. Instructions can be found here, [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup).
5. The remaining instructions assume you have an open terminal on a system with Claude Code and bash installed.

## 1. Configure Claude Code

Model names in AI-VERDE are prefixed with an identifier for your course or team, separated by a dash or a slash (e.g. `my-team-claude-sonnet-4-6` or `my-team/claude-sonnet-4-6`). Use the exact names from your model list; Anthropic's public model IDs (e.g. `claude-sonnet-4-6`) will not work.

### Option 1: `~/.claude/settings.json` (recommended)

Add the following `env` section to `~/.claude/settings.json` (create the file if it does not exist). Settings in this file apply every time you run Claude Code, in any terminal.

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://llm-api.cyverse.ai",
    "ANTHROPIC_API_KEY": "<your-ai-verde-api-key>",
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
    "ANTHROPIC_BASE_URL": "https://llm-api.cyverse.ai",
    "ANTHROPIC_API_KEY": "sk-xxxxxxxxxxxxxxxxxxxxxx",
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
export ANTHROPIC_BASE_URL="https://llm-api.cyverse.ai"
export ANTHROPIC_API_KEY="<your-ai-verde-api-key>"
export ANTHROPIC_DEFAULT_OPUS_MODEL="<model name for opus>"
export ANTHROPIC_DEFAULT_SONNET_MODEL="<model name for sonnet>"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="<model name for haiku>"
```

Exported variables only last for the current terminal session. To avoid re-entering them each session, add the lines to your shell profile (e.g. `~/.bashrc` or `~/.zshrc`), then source your shell profile.

!!! Note

    To obtain the AI-VERDE Anthropic Base URL, simply remove `/v1` (e.g. `https://llm-api.cyverse.ai/v1` => `https://llm-api.cyverse.ai`). If both `~/.claude/settings.json` and your shell set the same variable, the value in `~/.claude/settings.json` is used.

## 2. Start Claude Code

You can then run Claude Code.

```bash
claude
```

The first time Claude Code detects `ANTHROPIC_API_KEY`, it asks whether to use the custom API key. Select **Yes**. You can run `/status` inside Claude Code to confirm the base URL and API key it is using.

## If you need to change your `ANTHROPIC_API_KEY`

If for some reason you need to change your VERDE API Key, update `ANTHROPIC_API_KEY` wherever you set it in step 1 (`~/.claude/settings.json` or your shell profile), then restart Claude Code. If you previously declined the key prompt, Claude Code ignores the key without asking again; re-enable it with the **Use custom API key** option under `/config`.
