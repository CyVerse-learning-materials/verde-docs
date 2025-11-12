# Using AI-VERDE with Continue.dev (VS Code Extension)

Continue.dev is an open-source coding assistant for Visual Studio Code that provides inline AI help for code completion, refactoring, and documentation. By connecting it to AI-VERDE, you can securely use CyVerse-hosted and course-approved models without exposing your code to external services.


## Prerequisites

Before getting started, make sure you have:

1. **AI-VERDE API Key**  
   - Obtain your key by following the [AI-VERDE API Token Guide](../api/api-token.md).

2. **Model Information**  
   - View available models and their names in the [AI-VERDE Model Documentation](../api/api-key-models.md).

3. **Visual Studio Code Installed**  
   - Download and install VS Code from the [VS Code website](https://code.visualstudio.com/).

4. **Continue.dev Extension Installed**  
   - In VS Code, open the Extensions tab (`Ctrl+Shift+X` or `Cmd+Shift+X`), search for “Continue”, and click Install.  
   - For more details, visit the [Continue.dev website](https://continue.dev/).


## 1. Sign In and Access Continue

1. Open Visual Studio Code.  
2. In the sidebar, click on the Continue icon to open the panel.  
3. If prompted, sign in with your Continue account (you can use GitHub, Google, or create a free account).  
4. Once signed in, you’ll see the Continue chat interface and a Model tab.


## 2. Add AI-VERDE as a Model Provider

You can connect your AI-VERDE API Key directly from the [Continue.dev website](https://continue.dev/).

1. In the Continue sidebar, click the Model tab.  
2. Scroll down to the bottom and click “Create Model”.  
3. In the popup, use this as an example:

```bash
  name: AI-Verde
version: 1.0.0
schema: v1

models:
  - name: AI-Verde GPT-4o-mini 
    provider: openai
    model: litellm_proxy/[MODEL NAME]
    apiBase: https://llm-api.cyverse.ai/v1 #add this
    apiKey: ${{ inputs.[AI-VERDE API KEY] }}
    roles:
      - chat
```

1. Click "Save".  
2. Your new AI-VERDE model will appear in the model list in VS Code extenstion.

> **Tip:** You can add multiple AI-VERDE models if your course provides access to different ones. For example, a general model and a coding-focused model.


## 3. (Optional) Configure via JSON File

You can also edit the Continue configuration file manually for advanced customization.

1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).  
2. Type “Continue: Open Config File” and press "Enter".  
3. Add or replace your configuration with the example below:

```json
{
  "models": [
    {
      "title": "AI-VERDE GPT-4o-mini",
      "model": "litellm_proxy/[MODEL NAME]",
      "provider": "openai",
      "apiBase": "https://llm-api.cyverse.ai/v1",
      "apiKey": "[AI_VERDE_API_KEY]"
    }
  ]
}
```