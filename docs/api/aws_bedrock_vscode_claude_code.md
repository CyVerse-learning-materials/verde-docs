# Using VSCode Claude Code Extension with AI-VERDE

VSCode Claude Code Extension is an official extension from Anthropic for using Claude Code within VSCode. AI-VERDE can serve as the backend for the extension, routing requests through AI-VERDE's budget controls and guardrails to Anthropic Claude models hosted on AWS Bedrock.

## Prerequisites

1. Obtain your **AI-VERDE API key** and note the **AI-VERDE base URL**. The base URL used in the environment variables ends in `/bedrock` rather than `/v1`. [Instructions can be found here](api-token.md).
2. Note the **Claude model ID** for Opus, Sonnet, and Haiku. [Instructions for listing available models can be found here](api-key-models.md). Model names in AI-VERDE are prefixed with an identifier for your course or team, separated by a dash or a slash (e.g. `my-team-claude-sonnet-4-6` or `my-team/claude-sonnet-4-6`).
3. Install **VS Code**. Instructions can be found at [https://code.visualstudio.com/download](https://code.visualstudio.com/download).

## 1. Install the "Claude Code for VS Code" extension from Anthropic
Within the extension marketplace, a simple search for "Claude Code" yields the desired extension.

![extension_install](../assets/vscode_claude_code_extension_install.png)

## 2. Configuring "Claude Code for VS Code" extension

Go to the extension page.

![extension_page](../assets/vscode_claude_code_extension_page.png)

Click on the gear icon and select "Settings".

![extension_dropdown](../assets/vscode_claude_code_extension_gear_dropdown.png)

Find the setting entry "Claude Code: Disable Login Prompt" and check the box to enable it.

![extension_settings](../assets/vscode_claude_code_extension_settings_disable_login_prompt.png)

### Configuring Environment Variables

Next you will need to configure the extension to use AI-VERDE as the backend for Anthropic Claude models hosted on AWS Bedrock. Set these in the extension's own "Claude Code: Environment Variables" setting. The extension checks this setting before launching, so it is the reliable place for your AI-VERDE credentials; values in `~/.claude/settings.json` do not reach the extension's login check.

Find the setting entry "Claude Code: Environment Variables" and click on "Edit in settings.json".

![extension_settings](../assets/vscode_claude_code_extension_settings_env_var.png)

You will need to add the following environment variables to the `claudeCode.environmentVariables` section of the settings:

- add your AI-VERDE API key as the ANTHROPIC_AUTH_TOKEN
- add your Bedrock base URL as ANTHROPIC_BEDROCK_BASE_URL
- replace the model IDs with your own team model IDs for Opus, Sonnet, and Haiku

```json
    "claudeCode.environmentVariables": [
        { "name": "ANTHROPIC_AUTH_TOKEN", "value": "REPLACE_WITH_YOUR_API_KEY"},
        { "name": "ANTHROPIC_BEDROCK_BASE_URL", "value":"REPLACE_WITH_YOUR_BEDROCK_BASE_URL"},
        { "name": "CLAUDE_CODE_SKIP_BEDROCK_AUTH", "value":"1"},
        { "name": "CLAUDE_CODE_USE_BEDROCK", "value":"1"},
        { "name": "ANTHROPIC_DEFAULT_OPUS_MODEL", "value":"my-team-claude-opus-4-6"},
        { "name": "ANTHROPIC_DEFAULT_SONNET_MODEL", "value":"my-team-claude-sonnet-4-6"},
        { "name": "ANTHROPIC_DEFAULT_HAIKU_MODEL", "value":"my-team-claude-haiku-4-5"}
    ],
```

For example, with the values filled in:

```json
    "claudeCode.environmentVariables": [
        { "name": "ANTHROPIC_AUTH_TOKEN", "value": "sk-xxxxxxxxxxxxxxxxxxxxxx"},
        { "name": "ANTHROPIC_BEDROCK_BASE_URL", "value":"https://llm-api.cyverse.ai/bedrock"},
        { "name": "CLAUDE_CODE_SKIP_BEDROCK_AUTH", "value":"1"},
        { "name": "CLAUDE_CODE_USE_BEDROCK", "value":"1"},
        { "name": "ANTHROPIC_DEFAULT_OPUS_MODEL", "value":"my-team-claude-opus-4-6"},
        { "name": "ANTHROPIC_DEFAULT_SONNET_MODEL", "value":"my-team-claude-sonnet-4-6"},
        { "name": "ANTHROPIC_DEFAULT_HAIKU_MODEL", "value":"my-team-claude-haiku-4-5"}
    ],
```

!!! Note

    To obtain the AI-VERDE Bedrock Base URL, simply substitute `/v1` with `/bedrock`, e.g. `https://llm-api.cyverse.ai/v1` to `https://llm-api.cyverse.ai/bedrock`.

!!! Note

    This setting only applies to the VS Code extension. To use Claude Code in the terminal as well, configure it separately as described in [Using Claude Code](aws_bedrock_claude_code.md).

## 3. Restart VS Code

You may need to restart VS Code for the environment variables & settings to take effect.

## 4. Using the extension
The extension has chat functionality accessed from the leftmost bar in VS Code:

![chat](../assets/vscode_claude_code_chat_button.png)

You can also open a chat window by clicking on the Claude logo:

![code](../assets/vscode_claude_code_chat_icon.png)
