# Using Claude Code with AI-VERDE

Claude Code is Anthropic's official CLI coding assistant. AI-VERDE can serve as the backend for Claude Code, routing requests through AI-VERDE's budget controls and guardrails to Anthropic Claude models hosted on AWS Bedrock.

## Prerequisites

1. Obtain your **AI-VERDE API key** and note the **AI-VERDE base URL**. The base URL used in the environment variables ends in `/bedrock` rather than `/v1`. [Instructions can be found here](api-token.md).
2. Note the **Claude model ID** for Opus, Sonnet, and Haiku. [Instructions for listing available models can be found here](api-key-models.md).
3. Install **Claude Code**. Instructions can be found at [https://code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup).
4. The remaining instructions assume you have an open terminal with Claude Code installed on Linux or macOS.

## 1. Set the Environment Variables

Export the following environment variables before launching Claude Code.

```bash
export ANTHROPIC_AUTH_TOKEN="<your-ai-verde-api-key>"
export ANTHROPIC_BEDROCK_BASE_URL=https://llm-api.cyverse.ai/bedrock
export CLAUDE_CODE_SKIP_BEDROCK_AUTH=1
export CLAUDE_CODE_USE_BEDROCK=1
export ANTHROPIC_DEFAULT_OPUS_MODEL="<model name for opus>"
export ANTHROPIC_DEFAULT_SONNET_MODEL="<model name for sonnet>"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="<model name for haiku>"
```

For example:

```bash
export ANTHROPIC_AUTH_TOKEN="xyz"
export ANTHROPIC_BEDROCK_BASE_URL=https://llm-api.cyverse.ai/bedrock
export CLAUDE_CODE_SKIP_BEDROCK_AUTH=1
export CLAUDE_CODE_USE_BEDROCK=1
export ANTHROPIC_DEFAULT_OPUS_MODEL="my-team-claude-opus-4-6"
export ANTHROPIC_DEFAULT_SONNET_MODEL="my-team-claude-sonnet-4-6"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="my-team-claude-haiku-4-5"
```

!!! Note

    To obtain the AI-VERDE Bedrock Base URL, simply substitute `/v1` with `/bedrock`, e.g. `https://llm-api.cyverse.ai/v1` to `https://llm-api.cyverse.ai/bedrock`.

To avoid re-entering these each session, add the lines to your shell profile (e.g. `~/.bashrc` or `~/.zshrc`). Then, you can source your shell profile.

## 2. Launch Claude Code

Start Claude Code:

```bash
claude
```
