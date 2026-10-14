# Common API Errors

When the AI-VERDE API rejects a request, it returns an HTTP error status and a short JSON message. This page explains the errors you are most likely to see, what causes them, and whether you can fix them yourself or need to contact support.

Your client may show the raw JSON, a shortened message, or an exception name. Search the error text for the HTTP status (`401`, `403`, `404`, `429`, and so on) and the `type` field, then find the matching section below.

## Quick reference

| Status | What it usually means | Who can fix it |
| --- | --- | --- |
| `400` | The model name is wrong | You |
| `401` | Your API key is missing, mistyped, or expired | You, or support if the key has expired |
| `403` | Your course or team doesn't have access to that model | Support |
| `404` | The base URL or endpoint path is wrong | You |
| `429` with `budget_exceeded` | Your course or team has used up its budget | Support |
| `429` without `budget_exceeded` | The model is busy or temporarily unavailable | Wait and retry |
| `500` or `503` | The model provider is down or unreachable | Wait and retry, then support |

## What an error looks like

Most errors come back as JSON with an `error` object:

```json
{
	"error": {
		"message": "Authentication Error, No api key passed in.",
		"type": "auth_error",
		"param": "None",
		"code": "401"
	}
}
```

`message` describes the problem. `type` names the error category, but some errors leave it empty (`null` or the string `"None"`). `code` repeats the HTTP status. Rely on the HTTP status first and use the message for detail.

## 401 Unauthorized: the API key was rejected

AI-VERDE could not match your request to a valid API key. Common causes:

- The key is missing from the request, or the client reads it from an environment variable that isn't set in the current shell.
- The key was copied with extra spaces or a missing character.
- The key belongs to a course or team that has ended, so it has expired.

The message tells you which case you hit:

| Message starts with | Cause |
| --- | --- |
| `Authentication Error, No api key passed in.` | The client didn't send a key |
| `Authentication Error, Invalid proxy server token passed.` | The key doesn't match any AI-VERDE key |
| `Authentication Error - Expired Key.` | The key has expired |

To fix it, copy the key again from the **API Key** tab of your course details (see [Obtaining your AI-VERDE API Key](api-key.md)) and check that your client sends it. OpenAI-compatible clients send it as a bearer token:

```http
Authorization: Bearer <your-ai-verde-api-key>
```

You can test the key on its own with curl. If this returns your model list, the key works and the problem is in your client configuration:

```bash
curl -s "https://llm-api.cyverse.ai/v1/models" -H "Authorization: Bearer $VERDE_API_KEY"
```

Retrying with the same key won't help. If a freshly copied key still fails, or the key has expired, email [ai-verde-support@cyverse.org](mailto:ai-verde-support@cyverse.org).

!!! Note

    Claude Code on AWS Bedrock reads the key from `ANTHROPIC_AUTH_TOKEN`, not `ANTHROPIC_API_KEY`. Setting the wrong variable produces a `401`. See [Using Claude Code](aws_bedrock_claude_code.md).

### 401 from the model provider

Sometimes your key is fine and the `401` comes from the provider behind AI-VERDE, such as AWS Bedrock. In that case the message contains `litellm.AuthenticationError` followed by the provider's own error text. Getting a new API key won't fix this. Email support with the full error message.

## 400 Bad Request: the model name is wrong

AI-VERDE doesn't recognize the model you asked for:

```json
{
	"error": {
		"message": "/chat/completions: Invalid model name passed in model=claude-sonnet-5. Call `/v1/models` to view available models for your key.",
		"type": "None",
		"param": "None",
		"code": "400"
	}
}
```

This usually happens when you use the provider's public model name instead of the AI-VERDE name. Models provided for your course or team carry a course or team prefix, for example `my-team-claude-sonnet-5` or `my-team/claude-sonnet-5`. CyVerse-hosted models such as `gemma-4-26b-it` have no prefix.

Copy the exact name from your model list. [Getting a List of Models](api-key-models.md) shows how to find it in the course details or with the API.

If the message instead contains `litellm.NotFoundError` with a `404` status, AI-VERDE recognized the name but the provider couldn't find the model. Email support.

## 403 Forbidden: no access to that model

The model exists, but your key isn't allowed to use it:

```json
{
	"error": {
		"message": "key not allowed to access model. This key can only access models=['my-team-gemma-4-26b-it']. Tried to access my-team-claude-sonnet-5",
		"type": "key_model_access_denied",
		"param": "model",
		"code": "403"
	}
}
```

The message lists the models your key can use. Switch to one of those, or ask your instructor or [ai-verde-support@cyverse.org](mailto:ai-verde-support@cyverse.org) to add the model to your course or team. You may also see `team_model_access_denied` or `user_model_access_denied`, which mean the same thing at the team or user level.

## 429 Too Many Requests

A `429` has two very different causes. Read the message before you retry.

### Budget exceeded

Your course, team, or key has spent its budget:

```json
{
	"error": {
		"message": "Budget has been exceeded! Team=team-example Current cost: 10.5, Max budget: 10.0",
		"type": "budget_exceeded",
		"param": null,
		"code": "429"
	}
}
```

Look for `type: "budget_exceeded"` or `Budget has been exceeded` in the message. Retrying won't work. Requests resume after the budget resets or after CyVerse staff raise it. Instructors can't change budgets themselves, so email [ai-verde-support@cyverse.org](mailto:ai-verde-support@cyverse.org) and include the course or team name.

### Model busy or temporarily unavailable

If the message says `No deployments available` or `No healthy deployment available`, AI-VERDE has no capacity for that model right now. Messages containing `litellm.RateLimitError` mean the provider is throttling requests.

These clear up on their own. If the response includes a `Retry-After` header or says `Try again in <seconds> seconds`, wait that long before retrying. Otherwise, wait a little longer between each retry, or switch to another model from your list for now. If the error lasts more than an hour or so, email support.

## 404 Not Found: wrong URL

A request to a URL that AI-VERDE doesn't serve returns this instead of the usual `error` object:

```json
{
	"detail": "Not Found"
}
```

Almost always the base URL is wrong for the client you're using. Check it against this table:

| Client type | Base URL |
| --- | --- |
| OpenAI-compatible (Codex, OpenCode, Aider, Chatbox AI, OpenAI SDK) | `https://llm-api.cyverse.ai/v1` |
| Anthropic-style (Claude Code, Anthropic SDK) | `https://llm-api.cyverse.ai` |
| LangChain and LlamaIndex with `litellm_proxy` | `https://llm-api.cyverse.ai` |
| Claude Code on AWS Bedrock | `https://llm-api.cyverse.ai/bedrock` |

OpenAI-compatible clients add `/chat/completions` to the base URL themselves, so don't include it. A base URL that ends in `/v1/v1` or is missing `/v1` both produce `404`. See [Base URL and Authentication](index.md#base-url-and-authentication) for details.

A `405 Method Not Allowed` means the path exists but the client used the wrong HTTP method, for example `GET` on `/v1/chat/completions` instead of `POST`.

## 500 and 503: provider problems

These errors mean AI-VERDE received your request but couldn't reach the model provider.

| Status | Message contains | Meaning |
| --- | --- | --- |
| `500` | `litellm.APIConnectionError` | AI-VERDE couldn't connect to the provider |
| `503` | `litellm.ServiceUnavailableError` | The provider is down |
| `503` | `no_db_connection` | AI-VERDE's key database is briefly unreachable |

There's nothing to change on your side. Wait a few minutes and retry. If the error persists, email [ai-verde-support@cyverse.org](mailto:ai-verde-support@cyverse.org) with the model name, the time, and the full message.

## Errors in Python code

Python libraries turn these HTTP errors into exceptions. The exception name tells you which section above applies.

The OpenAI SDK raises exceptions by HTTP status, such as `AuthenticationError` for `401`, `PermissionDeniedError` for `403`, `NotFoundError` for `404`, and `RateLimitError` for `429`. A budget error and a busy-model error both raise `RateLimitError`, so check the exception message for `budget_exceeded` before retrying in a loop.

LangChain and LlamaIndex use LiteLLM under the hood, so you may see LiteLLM exception names:

| Exception | See |
| --- | --- |
| `litellm.AuthenticationError` | [401 Unauthorized](#401-unauthorized-the-api-key-was-rejected) |
| `litellm.PermissionDeniedError` | [403 Forbidden](#403-forbidden-no-access-to-that-model) |
| `litellm.NotFoundError` | [400 Bad Request](#400-bad-request-the-model-name-is-wrong) or [404 Not Found](#404-not-found-wrong-url) |
| `litellm.BudgetExceededError` | [Budget exceeded](#budget-exceeded) |
| `litellm.RateLimitError` | [Model busy or temporarily unavailable](#model-busy-or-temporarily-unavailable) |
| `litellm.ServiceUnavailableError`, `litellm.APIConnectionError` | [500 and 503](#500-and-503-provider-problems) |

## Contacting support

If none of the above fixes the problem, email [ai-verde-support@cyverse.org](mailto:ai-verde-support@cyverse.org) with:

- the full error message, including the HTTP status
- the model name you requested
- the tool or library you're using and its base URL
- roughly when the error happened

Don't include your API key in the email.
