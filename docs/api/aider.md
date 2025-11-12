# Aider
You can follow these instructions to use your AI-VERDE API Key after Aider, self-described "AI pair programming in your terminal". More information on installing and using Aider can be found here, [Aider website](https://aider.chat).

## Prerequisites
1. **AI-VERDE API Key**  
   - Obtain your key by following the [API Token guide](https://aiverde-docs.cyverse.ai/api/api-token/).  
2. **Model Information**  
   - Identify the model(s) you plan to use by reviewing the [AI-VERDE Model Documentation](https://aiverde-docs.cyverse.ai/api/api-key-models/).  
3. **Install Aider**  
   - Follow the official [Aider installation instructions](https://aider.chat/#getting-started/).  
4. **Terminal Access**  
   - These instructions assume you have a terminal open on a Linux system with Aider installed.

## 1. Configuring Aider

1. Create a `$HOME/.aider.conf.yml` file with the following contents
```
openai-api-key: insert-your-aiverde-api-key
openai-api-base: https://llm-api.cyverse.ai/v1
model: openai/insert-default-model
```
2. Replace `insert-your-aiverde-api-key` with AI-VERDE API Key. 
3. Replace the text `insert-default-model` with the AI-VERDE model.
   Example how the model feild would be set:
   - For the phi4 model → model: openai/phi4
   - For the nrp/phi4 model → model: openai/nrp/phi4

!!! Note
    This is the minimal configuration needed to connect Aider. If you want to set other configuration for any models, you add a `$HOME/.aider.model.metadata.json` file. Instructions on the configuration values that can be set in this file can be found at [aider model settings](https://aider.chat/docs/config/adv-model-settings.html). 

## 2. Running Aider
Run Aider with the following command:

```
aider
```

!!! Note
    You may get additional prompts if you're not in a git repo and if you have not configured your model further (see note above). You can also run aider with `aider --no-show-model-warnings` if you prefer to ignore model warnings

If you are successful entering Aider, congratulations!