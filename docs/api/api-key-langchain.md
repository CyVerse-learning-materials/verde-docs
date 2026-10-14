# Using your AI-VERDE API key to integrate with LangChain

## Prerequisites

1. Obtain your AI-VERDE API key. [Instructions can be found here](api-key.md).
2. Note the model name you want to use. [Instructions for listing available models can be found here](api-key-models.md).
3. Install Python 3 with `pip`.

## 1. Install LangChain Python libraries

```bash
pip install langchain-litellm
```

## 2. Write a Python script

Replace `[MODEL NAME]` with a model name from your model list, keeping the `litellm_proxy/` prefix (e.g. `litellm_proxy/gemma-4-26b-it`). LiteLLM's `litellm_proxy` provider takes the base URL without `/v1`.

```python
from langchain_litellm import ChatLiteLLM

llm = ChatLiteLLM(
    model="litellm_proxy/[MODEL NAME]",
    api_key="[AI-VERDE API KEY]",
    api_base="https://llm-api.cyverse.ai",
)

print(llm.invoke("Hello, world!"))
```

Alternatively, you can include the API key as an environment variable or secret to avoid storing it in plain text:

```python
import getpass
import os

if not os.environ.get("VERDE_API_KEY"):
    os.environ["VERDE_API_KEY"] = getpass.getpass("Enter AI-VERDE API key: ")
api_key = os.environ["VERDE_API_KEY"]

from langchain_litellm import ChatLiteLLM

llm = ChatLiteLLM(
    model="litellm_proxy/[MODEL NAME]",
    api_key=api_key,
    api_base="https://llm-api.cyverse.ai",
)

print(llm.invoke("Hello, world!"))
```
