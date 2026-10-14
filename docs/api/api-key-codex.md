# Codex

You can follow these instructions to use your AI-VERDE API key after installing Codex. More information on using Codex can be found here, [https://github.com/openai/codex](https://github.com/openai/codex).

## Prerequisites

1. Obtain your AI-VERDE API key. [Instructions can be found here](api-key.md).
2. Note the model name you want to use. [Instructions for listing available models can be found here](api-key-models.md). Coding agents work best with models that support tool use; see the "Supports Tools" column in [Current CyVerse Models](../models-current.md).
3. Install Codex. Instructions can be found here, [https://github.com/openai/codex](https://github.com/openai/codex).
4. The remaining instructions assume a terminal on macOS or Linux with bash and Codex installed. Windows notes are included where the steps differ.

## 1. Set up the Codex configuration file

Codex saves its configuration at `~/.codex/config.toml` (`%USERPROFILE%\.codex\config.toml` on Windows). Add the following content to the configuration file (replace lines in existing content where appropriate), replacing `<your-model-name>` with the model you'd like to use.

```toml
model = "<your-model-name>"
model_provider = "ai-verde"
model_reasoning_effort = "medium" # change this if you want to adjust the reasoning effort for the model
approvals_reviewer = "user" # change this if you want to adjust the reviewer for approvals, the other option is "auto_review"

[model_providers.ai-verde]
name = "ai-verde"
base_url = "https://llm-api.cyverse.ai/v1"
env_key = "VERDE_API_KEY"
wire_api = "responses"
stream_idle_timeout_ms = 600000 # 10 minutes
stream_max_retries = 5
request_max_retries = 4
```

For example, your existing `~/.codex/config.toml` file may look like this:

```toml
model = "gpt-5.6-sol"
model_reasoning_effort = "high"
approvals_reviewer = "auto_review"

[projects."/home/my_user/my_git_repo_1"]
trust_level = "trusted"
```

After the update, your `~/.codex/config.toml` file should look like this:

```toml
model = "gemma-4-26b-it"
model_provider = "ai-verde"
model_reasoning_effort = "medium"
approvals_reviewer = "user"

[model_providers.ai-verde]
name = "ai-verde"
base_url = "https://llm-api.cyverse.ai/v1"
env_key = "VERDE_API_KEY"
wire_api = "responses"
stream_idle_timeout_ms = 600000 # 10 minutes
stream_max_retries = 5
request_max_retries = 4

[projects."/home/my_user/my_git_repo_1"]
trust_level = "trusted"
```

Export the following environment variable before launching Codex (replacing `<your-ai-verde-api-key>` with your AI-VERDE API key).

```bash
export VERDE_API_KEY="<your-ai-verde-api-key>"
```

To avoid re-entering this each session, add the line to your shell profile (e.g. `~/.bashrc` or `~/.zshrc`). Then, you can source your shell profile.

!!! Tip

    On Windows, set the variable permanently in PowerShell with `setx VERDE_API_KEY "<your-ai-verde-api-key>"`, then open a new terminal before launching Codex.

Alternatively, you can save the key in `~/.codex/.env` (`%USERPROFILE%\.codex\.env` on Windows), which Codex loads on startup, instead of exporting it:

```bash
VERDE_API_KEY=sk-xxx
```

This file holds your API key, so don't commit or share it.

## 2. Start Codex

You can then run Codex.

```bash
codex
```

## If you need to change your `VERDE_API_KEY`

If for some reason you need to change your AI-VERDE API key, update `VERDE_API_KEY` wherever you set it (your shell profile or `~/.codex/.env`), then restart Codex.
