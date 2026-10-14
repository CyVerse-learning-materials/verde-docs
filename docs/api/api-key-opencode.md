# OpenCode

[OpenCode](https://github.com/anomalyco/opencode) is an open-source AI coding agent for the terminal. It can read and edit code in your project and run commands, using any model you configure.

## Prerequisites

1. Obtain your AI-VERDE API key. [Instructions can be found here](api-key.md).
2. Note the model name(s) you want to use. [Instructions for listing available models can be found here](api-key-models.md). Coding agents work best with models that support tool use; see the "Supports Tools" column in [Current CyVerse Models](../models-current.md).
3. Install OpenCode. Instructions can be found here, [https://opencode.ai/](https://opencode.ai/).
4. The remaining instructions assume a terminal on macOS or Linux with bash and OpenCode installed.

## 1. Set up the OpenCode configuration file

OpenCode uses a configuration file to define custom providers and models. The configuration file is located at either of the following locations:

- (Mac/Linux) `~/.config/opencode/opencode.json`
- (Mac/Linux) `~/.config/opencode/opencode.jsonc` (`jsonc` is a superset of `json` that allows comments)

Here is an example configuration file for OpenCode that uses the AI-VERDE provider and models:

```jsonc
{
  "provider": {
    "ai-verde": { // this is the identifier for the provider, you can choose any name you like, it needs to be unique in the provider list
      "name": "AI-VERDE", // this is the display name of the provider (what is shown by the `/models` command), you can choose any name you like
      "npm": "@ai-sdk/openai-compatible", // this is the npm package that provides the provider's API, use `@ai-sdk/openai-compatible` unless you know what you are doing
      "models": {
        "gemma-4-26b-it": { // this is the model name shown in AI-VERDE
            "name": "my-gemma-4-26b-it" // this is the display name of the model (what is shown by the `/models` command), you can choose any name you like
        }
      },
      "options": {
        "apiKey": "{env:VERDE_API_KEY}", // reads your AI-VERDE API key from the VERDE_API_KEY environment variable
        "baseURL": "https://llm-api.cyverse.ai/v1", // this is the base URL for AI-VERDE, copy-paste from the same page where you got your API Key
        "timeout": 600000 // optional, this is the timeout in milliseconds for API requests, default is 600000 (10 minutes)
      }
    }
  },
  "$schema": "https://opencode.ai/config.json"
}
```

Then export your API key before launching OpenCode (replacing `<your-ai-verde-api-key>` with your AI-VERDE API key):

```bash
export VERDE_API_KEY="<your-ai-verde-api-key>"
```

To avoid re-entering this each session, add the line to your shell profile (e.g. `~/.bashrc` or `~/.zshrc`), then source your shell profile.

## 2. Start OpenCode

You can then run OpenCode.

```bash
opencode
```

Run `/models` and select the model you want to use. Run `/models` again to switch models during a session.

## If you need to change your API Key

If for some reason you need to change your AI-VERDE API key, re-set the `VERDE_API_KEY` environment variable (and your shell profile, if you added it there), then restart OpenCode.
