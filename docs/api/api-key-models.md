# Getting a List of Models

There are three ways to obtain a list of models:

1. Go to [this page](../models-current.md) to view the list of CyVerse models. This list does not include models from external inference services e.g., Jetstream2.
2. Viewing your models in the Course Details.
3. Using your API Key to view your models.

Models hosted by CyVerse (listed on [Current CyVerse Models](../models-current.md)) have no prefix, e.g. `gemma-4-26b-it`. Models provided for your course or team are prefixed with an identifier for your course or team, separated by a dash or a slash (e.g. `my-team-claude-sonnet-5` or `my-team/claude-sonnet-5`). Always use the exact name from your model list.

## Viewing your models in the Course Details

Your available models will be visible in the AI-VERDE application. These are the steps:

1. Go to [https://chat.cyverse.ai](https://chat.cyverse.ai).
2. After successfully logging in, click the Details button of your course.
3. Click the "API Key" tab.
4. The "Available Models" section lists all the models your course has access to.

## Using your API Key to view your models

After obtaining your API key from your course/team, store it in an environment variable:

```bash
export VERDE_API_KEY="<your-ai-verde-api-key>"
```

Then list your available models using curl:

```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" -H "Authorization: Bearer $VERDE_API_KEY" -H 'Content-Type: application/json'
```

Alternatively, you can use `jq` or python's json module to view the output in a more human readable format.

Option 1: If you have `jq` installed:

```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" -H "Authorization: Bearer $VERDE_API_KEY" -H 'Content-Type: application/json'|jq
```

Option 2: If you have Python installed (`json.tool` is part of the standard library):

```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" -H "Authorization: Bearer $VERDE_API_KEY" |python -m json.tool
```
