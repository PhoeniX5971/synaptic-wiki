---
title: DeepSeek Adapter
sidebar_position: 16
---

# DeepSeekAdapter

Adapter for DeepSeek-powered OpenAI endpoints. Handles conversion of Synaptic tools, history management, and content generation via the DeepSeek API.

---

## Example

```python
from synaptic.core.provider.deepseek import DeepSeekAdapter
from synaptic.core.base.memory import History, ResponseFormat
from synaptic.core.tool import Tool
from datetime import datetime

history = History()
tools = [Tool(name="greet", declaration={"name": "greet", "description": "Greets a user", "parameters": {"type": "object", "properties": {"name": {"type": "string"}}, "required": ["name"]}})]

adapter = DeepSeekAdapter(
    model="deepseek-r1",
    history=history,
    api_key="YOUR_API_KEY",
    response_format=ResponseFormat.NONE,
    response_schema=None,
    temperature=0.7,
    tools=tools
)

response = adapter.invoke("Hello DeepSeek!")
print(response.message)
```

---

## Class hierarchy

```
BaseModel
 └── DeepSeekAdapter
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [History](/api/core/base/history), [ResponseMem](/api/core/base/response-memory), [Tool](/api/core/tool)

---

## Constructor

### DeepSeekAdapter(model: str, ...)

| Name              | Type                                                      | Description                                                      | Default |
| ----------------- | --------------------------------------------------------- | ---------------------------------------------------------------- | ------- |
| `model`           | **str**                                                   | DeepSeek OpenAI model to use                                     | —       |
| `history`         | **[History](/api/core/base/history)**                     | Conversation history manager                                     | —       |
| `api_key`         | **str**                                                   | API key for DeepSeek                                             | —       |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Desired structured response format                               | —       |
| `response_schema` | **Any**                                                   | JSON schema for structured responses (if `JSON` response_format) | —       |
| `temperature`     | **float**                                                 | Sampling temperature                                             | 0.8     |
| `tools`           | **list\[[Tool](/api/core/tool)\]**, optional              | Synaptic tools to bind                                           | None    |

---

## Object properties

| Property          | Type                                                      | Description                                  |
| ----------------- | --------------------------------------------------------- | -------------------------------------------- |
| `client`          | **OpenAI**                                                | DeepSeek API client (OpenAI-compatible)      |
| `model`           | **str**                                                   | Name of the DeepSeek model                   |
| `synaptic_tools`  | **list\[[Tool](/api/core/tool)\]**                        | Synaptic tools attached to this adapter      |
| `openai_tools`    | **list\[dict\]**                                          | Converted OpenAI/DeepSeek tool definitions   |
| `temperature`     | **float**                                                 | Sampling temperature                         |
| `history`         | **[History](/api/core/base/history)**                     | Conversation history                         |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Response format type                         |
| `response_schema` | **Any**                                                   | Schema for structured responses              |
| `role_map`        | **dict\[str,str\]**                                       | Maps Synaptic roles to OpenAI/DeepSeek roles |

---

## Object methods

### invoke(prompt: str, ...) → [ResponseMem](/api/core/base/response-memory)

Generate a response using DeepSeek.

| Parameter  | Type    | Description                                    |
| ---------- | ------- | ---------------------------------------------- |
| `prompt`   | **str** | User or system message                         |
| `role`     | **str** | Must be `"user"`, `"assistant"`, or `"system"` |
| `**kwargs` | —       | Additional parameters for DeepSeek API call    |

**`Returns:`** **[ResponseMem](/api/core/base/response-memory)** object containing the assistant message and any tool calls.

---

### to_messages() → list\[ChatCompletionMessageParam\]

Convert conversation history to OpenAI-compatible ChatCompletion message objects.

**`Returns:`** List of chat messages suitable for DeepSeek API input.

---

### \_invalidate_tools() _(internal)_

Update OpenAI/DeepSeek tool definitions without mutating the Synaptic tools.

---

### \_convert_tools() → None _(internal)_

Convert Synaptic [`Tool`](/api/core/tool) objects and global [`TOOL_REGISTRY`](/api/core/tool#object-properties) to OpenAI/DeepSeek function definitions.

---
