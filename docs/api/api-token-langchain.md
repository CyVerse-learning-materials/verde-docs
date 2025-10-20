# Using your AI-VERDE API key to integrate with LangChain

## 1. Install LangChain Python Libraries

To begin integrating AI-VERDE with LangChain, install the required Python package:

```bash
pip install langchain_community
```

## 2. Obtain variables to integrate AI-VERDE with LangChain

You will need your AI-VERDE APIKey to connect LangChain to the CyVerse API.

**AI-VERDE API Key and API URL**  
    - Obtain your credentials by following the [AI-VERDE API Token Guide](api-token.md).  

Once you have your key, you can view the models you have access to (identified by their `id`) with the following command:
```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" \
-H "Authorization: Bearer [AI-VERDE API KEY]" \
-H 'Content-Type: application/json' | jq
```
## 3. Create python scripts
You can now connect AI-VERDE to LangChain using the following Python example.
Before running the script, make sure to:
- Replace `[MODEL NAME]` with one of your available model IDs.
- Replace `[AI-VERDE API KEY]` with your personal API key

```python
from langchain_community.chat_models import ChatLiteLLM

llm = ChatLiteLLM(
    model="litellm_proxy/[MODEL NAME]",
    api_key="[AI-VERDE API KEY]",
    api_base="https://llm-api.cyverse.ai")

print (llm.invoke("Hello, world!"))
```


To keep your API key secure, you can store it as an `environment variable` instead of typing it directly into your script. This ensures your credentials remain private if you share or upload your code.

```python
import getpass
import os

if not os.environ.get("AIVERDE_API_KEY"):
  os.environ["AIVERDE_API_KEY"] = getpass.getpass("Enter AI-VERDE API key: ")
api_key = os.environ["AIVERDE_API_KEY"]

from langchain_community.chat_models import ChatLiteLLM

llm = ChatLiteLLM(
    model="litellm_proxy/[MODEL NAME]",
    api_key=api_key,
    api_base="https://llm-api.cyverse.ai")

print (llm.invoke("Hello, world!"))
```