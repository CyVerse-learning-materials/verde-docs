# Getting a List of Models

This page explains how to find which AI models are available to you in **AI-VERDE**.  
You can view your models directly in the application or through a simple command-line request using your API Key.

## Ways to View Available Models

1. **From the Models Page** – Visit [this page](../models-current.md) to see the list of CyVerse models.  
   > *Note:* This list only includes CyVerse-hosted models. External models (e.g., Jetstream2) are not shown.

2. **From Your Course Details** – View your available models directly in your AI-VERDE course.

3. **Using Your API Key** – Retrieve a detailed list of models through the command line.


## Viewing Models in the Course Details

1. Go to [https://chat.cyverse.ai](https://chat.cyverse.ai)  
2. Log in with your CyVerse credentials  
3. Click "Details" on your course  
4. Select the "API Key" tab  
5. The "Available Models" section will display all models your course can access  


## Viewing Models Using Your API Key

After obtaining your "API Key" from your course or team, you can run the following command in your terminal to request a list of all models available to you.  
This command uses `curl` to securely connect to the CyVerse API and return your model list in JSON format:

```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-H 'Content-Type: application/json'
```


The response from the API is returned in JSON format, which can appear as a single long block of text.  To make it easier to read, you can format the output using tools like `jq` or Python’s built-in `json` module.


**Option 1: Using `jq`**

If you have the `jq` command-line tool installed, it will organize the JSON output into a clean, readable structure:

```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
-H 'Content-Type: application/json' | jq
```

**Option 2: Using Python’s Built-in JSON Module**

If you have Python installed, you can use its built-in JSON parser to format the output neatly:

```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" \
-H "Authorization: Bearer $OPENAI_API_KEY" \
| python -m json.tool
```