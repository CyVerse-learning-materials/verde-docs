# Introduction to AI-VERDE API

AI-VERDE exposes an OpenAI-compatible API, so any tool or library that supports OpenAI can connect to it using your AI-VERDE API key. AI-VERDE also accepts Anthropic-style requests (used by Claude Code and the Anthropic SDK) and, for Claude Code only, AWS Bedrock-style requests for Claude models hosted on AWS Bedrock. This section explains how to get your key and use it across a range of environments.

## Getting Started

Before using the API you will need to:

1. **Obtain your API key** — Sign in at [chat.cyverse.ai](https://chat.cyverse.ai), open your course or team details, and copy the key from the **API Key** tab. See [Obtaining your AI-VERDE API Key](api-token.md) for step-by-step instructions.
2. **Know which models are available** — Your available models are listed on the same API Key page. You can also retrieve them programmatically; see [Getting a List of Models](api-key-models.md).

## What's in This Section

| Section                                                            | What it covers                                                                                 |
| ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| [Using Your API Key for AWS Bedrock Models](aws_bedrock.md)        | Claude models on AWS Bedrock with Claude Code and the Claude Code for VS Code extension            |
| [Using Your API Key in Code](api-token-langchain.md)               | Python integration with LangChain, LlamaIndex, and the Anthropic Python SDK                    |
| [Using CLI Coding Assistants](claude-code-router.md)               | Terminal-based AI coding tools: Claude Code Router, Aider, Claude Code, Codex, and OpenCode     |
| [Using IDEs](api-token-vscode.md)                                  | Editor integration for VSCode                                                                  |
| [Using Desktop Clients](chatboxai.md)                              | GUI chat clients such as ChatboxAI                                                             |

## Base URL and Authentication

When configuring a client, you need your **API key** (copied from the AI-VERDE dashboard) and a **base URL**. The base URL depends on which style of API the client speaks:

| API style         | Base URL                             | Used by                                                                                                                                                             |
| ----------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OpenAI-compatible | `https://llm-api.cyverse.ai/v1`      | [Aider](aider.md), [Codex](api-key-codex.md), [OpenCode](api-key-opencode.md), [Claude Code Router](claude-code-router.md), [ChatboxAI](chatboxai.md), [VSCode](api-token-vscode.md), and most OpenAI clients |
| Anthropic-style   | `https://llm-api.cyverse.ai`         | [Claude Code (Anthropic models)](api-key-claude.md), [Claude Code (non-Anthropic models)](api-key-claude-non-anthropic.md), [Anthropic Python SDK](aws_bedrock_anthropic_sdk_py.md) |
| AWS Bedrock       | `https://llm-api.cyverse.ai/bedrock` | [Claude Code on Bedrock](aws_bedrock_claude_code.md), [Claude Code for VS Code on Bedrock](aws_bedrock_vscode_claude_code.md)                                         |

If your course details show a different base URL ending in `/v1`, use it for OpenAI-compatible clients, remove `/v1` for Anthropic-style clients, and replace `/v1` with `/bedrock` for AWS Bedrock.

!!! Note

    The [LangChain](api-token-langchain.md) and [LlamaIndex](api-token-llamaindex.md) examples use LiteLLM's `litellm_proxy` provider, which takes the base URL without `/v1` (`https://llm-api.cyverse.ai`).

OpenAI-compatible clients send the API key as a bearer token (`Authorization: Bearer <your-api-key>`), and Anthropic-style clients may send it in an `x-api-key` header instead; AI-VERDE accepts either. Each guide shows which setting or environment variable holds the key for that tool.
