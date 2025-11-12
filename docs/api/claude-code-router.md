# Claude Code Router (using non-Anthropic Models)
This guide explains how to connect Claude Code with AI-VERDE using the Claude Code Router. By linking your AI-VERDE API key and model, you can route requests from Claude Code to non-Anthropic models  through AI-VERDE.
 
For more details on installation and usage, see the [Claude Code Router GitHub page](https://github.com/musistudio/claude-code-router).

## Prerequisites

1. **AI-VERDE API Key**  
   - Obtain your key by following the [AI-VERDE API Token Guide](https://aiverde-docs.cyverse.ai/api/api-token/).  

2. **Model Information**  
   - Identify the model(s) you plan to configure by reviewing the [AI-VERDE Model Documentation](https://aiverde-docs.cyverse.ai/api/api-key-models/).  

3. **Claude Code Installed**  
   - Follow the [Claude Code Installation Instructions](https://www.anthropic.com/claude-code/).  

4. **Claude Code Router Installed**  
   - Install the router by following the [Claude Code Router Setup Guide](https://github.com/musistudio/claude-code-router).  

5. **Terminal Access**  
   - Ensure you are using a terminal with Claude Code and bash available.

## 1. Starting Claude Code Router
This step should only be needed the first time you use Claude Code Router.
In a terminal, enter the command `ccr start`
```
$ ccr start
```

## 2. Configuring Claude Code Router
After starting the router, run:
```
ccr code
```
You will be prompted to enter configuration details.
Use the table below as a reference for what to enter in each field:

| Field | Value or Instructions | Notes |
| ------| --------------------- | ----- |
| Provider Name | `ai-verde` | any name works |
| Provider API KEY | enter your AI-VERDE API key | copy from your account | 
| Provider URL | `https://llm-api.cyverse.ai/v1/chat/completions` |default AI-VERDE API endpoint.|
| MODEL Name | `<verde model name>` | replace `<verde model name>` with the model you'd like to use |

After entering your model information, you should see output similar to:
```
Loaded JSON config from: /root/.claude-code-router/config.json
register transformer: Anthropic (endpoint: /v1/messages)
register transformer: gemini (endpoint: /v1beta/models/:modelAndAction)
register transformer: deepseek (no endpoint)
register transformer: tooluse (no endpoint)
register transformer: openrouter (no endpoint)
register transformer: maxtoken (no endpoint)
providerConfig:  ai-verde undefined
ai-verde provider registered
🚀 LLMs API server listening on http://127.0.0.1:3456
```
Once you see the message confirming registration, press `Ctrl + C` to stop the process before running Claude Code with Claude Code Router.

## 3. Running Claude Code Router
Running Claude Code with Claude Code Router with the following command:

```
ccr code
```

If successful, you’ll enter Claude Code with your AI-VERDE configuration active. To use the same setup again, simply run `ccr code` each time you start a new session.

## Updating Claude Code Router configuration
You can update your configuration at any time — for example, to add new models or change API settings. To edit your setup manually, open the configuration file located at: 
```bash
~/.claude-code-router/config.json`
```
Make your desired changes, save, and restart Claude Code Router to apply the updates.