# Using Anthropic Python SDK with AI-VERDE

[Anthropic Python SDK](https://github.com/anthropics/anthropic-sdk-python) is Anthropic's official Python SDK for interacting with Claude models. AI-VERDE can serve as the backend for the Anthropic Python SDK, routing requests through AI-VERDE's budget controls and guardrails to the Claude models available to your course or team.

!!! Note

    The Anthropic Python SDK uses AI-VERDE's Anthropic-style API at `https://llm-api.cyverse.ai`. It does not use the `/bedrock` endpoint, which is reserved for [Claude Code](aws_bedrock_claude_code.md), even when your Claude models are hosted on AWS Bedrock.

## Prerequisites

1. Obtain your **AI-VERDE API key** and note the **AI-VERDE base URL**. The base URL used in the script must have the `/v1` suffix removed, if present. [Instructions can be found here](api-key.md).
2. Note the **Claude model ID** you want to use. [Instructions for listing available models can be found here](api-key-models.md). Model names in AI-VERDE are prefixed with an identifier for your course or team, separated by a dash or a slash (e.g. `my-team-claude-sonnet-4-6` or `my-team/claude-sonnet-4-6`).
3. Install **Anthropic Python SDK**. Instructions can be found at [https://github.com/anthropics/anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python).

## Example Python script using Anthropic Python SDK with AI-VERDE

Export the following environment variables for your script.

```bash
export ANTHROPIC_API_KEY="<your-ai-verde-api-key>"
```

For example:

```bash
export ANTHROPIC_API_KEY="sk-xyz"
```

Example script:

```python
import os
from anthropic import Anthropic

client = Anthropic(
    base_url="https://llm-api.cyverse.ai", # Replace with the AI-VERDE base URL if different
    api_key=os.environ.get("ANTHROPIC_API_KEY"),
)

message = client.messages.create(
    max_tokens=128,
    messages=[
        {
            "role": "user",
            "content": "Hello, Claude",
        }
    ],

    model="<model name>", # Replace with a Claude model name from your model list
)

print(message.content)
```

!!! Note

    To obtain the AI-VERDE Anthropic Base URL, strip the `/v1` suffix if present.
