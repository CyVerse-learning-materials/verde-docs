# Using AI-VERDE with AWS Bedrock

AWS Bedrock is Amazon's fully managed service for accessing foundation models from leading AI providers. AI-VERDE allows users to use AWS Bedrock-provided Anthropic Claude models with Claude Code, both in the terminal and in the VS Code extension.

!!! Note

    Currently, the subsequent instructions focus on using Anthropic Claude models from AWS Bedrock. As other models are provided, the instructions will be updated.

## Prerequisites

Before connecting Claude Code to AI-VERDE, you will need:

- An **AI-VERDE API key** — sign in at [chat.cyverse.ai](https://chat.cyverse.ai), open your course or team details, and copy the key from the **API Key** tab. See [Obtaining your AI-VERDE API Key](api-key.md) for step-by-step instructions.
- The **AI-VERDE Bedrock base URL**: `https://llm-api.cyverse.ai/bedrock` (or the URL shown in your course details, with `/v1` replaced by `/bedrock`).

## How It Works

AI-VERDE acts as a proxy between your application and the underlying model. When you send a request to the AI-VERDE endpoint, AI-VERDE authenticates it against your team or course budget, applies any configured guardrails, then forwards the request to the appropriate model — which may be hosted on AWS Bedrock. For Claude Code, AI-VERDE exposes a Bedrock-compatible endpoint at `/bedrock`, so Claude Code can use its built-in Bedrock support while AI-VERDE handles authentication and budgets. Other clients should use AI-VERDE's OpenAI-compatible or Anthropic-style endpoints instead; see [Base URL and Authentication](index.md#base-url-and-authentication).

!!! Note

    The Bedrock-style endpoint is only intended for Claude Code. To call Claude models from your own code, use the [Anthropic Python SDK](aws_bedrock_anthropic_sdk_py.md), which uses the Anthropic-style API.
