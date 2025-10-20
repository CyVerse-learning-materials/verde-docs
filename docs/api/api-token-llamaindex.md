# Using your AI-VERDE API key to integrate with LlamaIndex

## 1. Install LlamaIndex libraries
Install the required Python packages for LlamaIndex and LiteLLM integration:
```bash
pip install llama-index-core llama-index-llms-litellm
```

## 2. Obtain variables to integrate AI-VERDE with LangChain

You’ll need your AI-VERDE API key and model ID to connect to the API. Instructions for obtaining them are available here:

**AI-VERDE API Key and API URL**  
    - Obtain your credentials by following the [AI-VERDE API Token Guide](api-token.md).  

**Model Information**  
    - Review the models you plan to use in the [AI-VERDE Model Access Documentation](api-key-models.md).  

Once you have your key, you can view the models you have access to (identified by their `id`) with the following command:
```bash
curl -s -L "https://llm-api.cyverse.ai/v1/models" \
-H "Authorization: Bearer [AI-VERDE API KEY]" \
-H 'Content-Type: application/json' | jq
```

## 3. Write python scripts
Below is a Python example to test your connection to AI-VERDE using LlamaIndex.
Before running the script, make sure to:
- Replace `[MODEL NAME]` with one of your available model IDs.
- Replace `[AI-VERDE API KEY]` with your personal API key

```python
from llama_index.llms.litellm import LiteLLM
from llama_index.core.llms import ChatMessage

llm = LiteLLM(
    model="litellm_proxy/[MODEL NAME]",
    api_base="https://llm-api.cyverse.ai",
    api_key="[AI-VERDE API KEY]",)

message = ChatMessage(role="user", content="Hey! how's it going?")
response = llm.chat([message])

print(response)
```

To keep your API key secure, you can store it as an `environment variable` instead of typing it directly into your script. This ensures your credentials remain private if you share or upload your code.

```python
import getpass
import os

if not os.environ.get("AIVERDE_API_KEY"):
  os.environ["AIVERDE_API_KEY"] = getpass.getpass("Enter AI-VERDE API key: ")
api_key = os.environ["AIVERDE_API_KEY"]

from llama_index.llms.litellm import LiteLLM
from llama_index.core.llms import ChatMessage

llm = LiteLLM(
    model="litellm_proxy/[MODEL NAME]",
    api_base="https://llm-api.cyverse.ai",
    api_key="[AI-VERDE API KEY]",)

message = ChatMessage(role="user", content="Hey! how's it going?")
response = llm.chat([message])

print(response)
```

!!! Note "Llama Index embedding support is outlined [here](https://docs.llamaindex.ai/en/stable/api_reference/embeddings/litellm/#llama_index.embeddings.litellm.LiteLLMEmbedding), but functionality depends on access to an embedding model through AI-VERDE."
