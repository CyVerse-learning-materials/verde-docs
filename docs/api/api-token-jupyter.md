# Examples of using your AI-VERDE API Token in Jupyter
This guide explains how to set up and use your AI-VERDE API Key inside Jupyter Notebook Once configured, you can send prompts, run code, and receive AI responses directly within your notebook.

## Prerequisites

1. **AI-VERDE API Key**  
   - Obtain your key by following the [AI-VERDE API Token Guide](https://aiverde-docs.cyverse.ai/api/api-token/).

2. **Model Information**  
   - View available models and their names in the [AI-VERDE Model Documentation](../api/api-key-models.md).

3. **Jupyter Installed**  
   - For intstalling Jupyter, visit [Jupyter Installation Website](https://jupyter.org/install).

## 1. Open Jupyter Notebook

After installing Jupyter, start it by running this command in your terminal:
```bash
jupyter notebook
```

## Add Your AI-VERDE API KEY

**Option 1** — Save It to Your System
This keeps your key private and reusable.

```bash
export AIVERDE_API_KEY="your_api_key_here"
```

**Option 2** — Enter It Inside the Notebook
If you prefer to enter it manually each time, use this in a new cell:

```bash
import os, getpass

if not os.getenv("AIVERDE_API_KEY"):
    os.environ["AIVERDE_API_KEY"] = getpass.getpass("Enter your AI-VERDE API Key: ")
```
## Test the Connection 
Now, let’s make sure your API key works. If everything works, you’ll see a list of available models. 
```bash
import os, requests, json

API_URL = "https://llm-api.cyverse.ai/v1/models"
api_key = os.getenv("AIVERDE_API_KEY")

headers = {"Authorization": f"Bearer {api_key}"}
response = requests.get(API_URL, headers=headers)

print("Status Code:", response.status_code)
print(json.dumps(response.json(), indent=2))
```

## Send a Test Prompt to AI-VERDE
Use one of your models to send a message and enter your model ID

```bash
import os, requests, json

API_URL = "https://llm-api.cyverse.ai/v1/"
api_key = os.getenv("AIVERDE_API_KEY")

headers = {
    "Authorization": f"Bearer {api_key}",
    "Content-Type": "application/json"
}
data = {
    "model": "litellm_proxy/[MODEL NAME]",  # Replace with your model ID
    "messages": [
        {"role": "user", "content": "Hello AI-VERDE! What can you do?"}
    ]
}
response = requests.post(API_URL, headers=headers, json=data)
result = response.json()

# Display the model's response
print(result["choices"][0]["message"]["content"])
```