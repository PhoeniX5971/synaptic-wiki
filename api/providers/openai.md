---
title: OpenAI Adapter
sidebar_position: 15
---

# OpenAIAdapter

Adapter for OpenAI models. Handles conversion of Synaptic tools, history management, and content generation via the OpenAI API.

---

## Example

```python
from synaptic.core.provider.openai import OpenAIAdapter
from synaptic.core.base.memory import History, ResponseFormat
from synaptic.core.tool import Tool
from datetime import datetime

history = History()
tools = [Tool(name="greet", declaration={"name": "greet", "description": "Greets a user", "parameters": {"type": "object", "properties": {"name": {"type": "string"}}, "required": ["name"]}})]

adapter = OpenAIAdapter(
    model="gpt-4",
    history=history,
    api_key="YOUR_API_KEY",
    response_format=ResponseFormat.NONE,
    response_schema=None,
    temperature=0.7,
    tools=tools
)

response = adapter.invoke("Hello OpenAI!")
print(response.message)
```

---

## Class hierarchy

```
BaseModel
 └── OpenAIAdapter
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [History](/api/core/base/history), [ResponseMem](/api/core/base/response-memory), [Tool](/api/core/tool)

---

## Constructor

### OpenAIAdapter(model: str, ...)

| Name              | Type                                                      | Description                                                      | Default |
| ----------------- | --------------------------------------------------------- | ---------------------------------------------------------------- | ------- |
| `model`           | **str**                                                   | OpenAI model to use                                              | —       |
| `history`         | **[History](/api/core/base/history)**                     | Conversation history manager                                     | —       |
| `api_key`         | **str**                                                   | API key for OpenAI                                               | —       |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Desired structured response format                               | —       |
| `response_schema` | **Any**                                                   | JSON schema for structured responses (if `JSON` response_format) | —       |
| `temperature`     | **float**                                                 | Sampling temperature                                             | 0.8     |
| `tools`           | **list\[[Tool](/api/core/tool)\]**, optional              | Synaptic tools to bind                                           | None    |

---

## Object properties

| Property          | Type                                                      | Description                             |
| ----------------- | --------------------------------------------------------- | --------------------------------------- |
| `client`          | **OpenAI**                                                | OpenAI API client                       |
| `model`           | **str**                                                   | Name of the OpenAI model                |
| `synaptic_tools`  | **list\[[Tool](/api/core/tool)\]**                        | Synaptic tools attached to this adapter |
| `openai_tools`    | **list\[dict\]**                                          | Converted OpenAI tool definitions       |
| `temperature`     | **float**                                                 | Sampling temperature                    |
| `history`         | **[History](/api/core/base/history)**                     | Conversation history                    |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Response format type                    |
| `response_schema` | **Any**                                                   | Schema for structured responses         |
| `role_map`        | **dict\[str,str\]**                                       | Maps Synaptic roles to OpenAI roles     |

---

## Object methods

### invoke(prompt: str, ...) → [ResponseMem](/api/core/base/response-memory)

Generate a response using OpenAI.

| Parameter  | Type    | Description                                    |
| ---------- | ------- | ---------------------------------------------- |
| `prompt`   | **str** | User or system message                         |
| `role`     | **str** | Must be `"user"`, `"assistant"`, or `"system"` |
| `**kwargs` | —       | Additional parameters for OpenAI API call      |

**`Returns:`** **[ResponseMem](/api/core/base/response-memory)** object containing the assistant message and any tool calls.

---

### to_messages() → list\[ChatCompletionMessageParam\]

Convert conversation history to OpenAI ChatCompletion message objects.

**`Returns:`** List of OpenAI chat messages suitable for API input.

---

### \_invalidate_tools() _(internal)_

Update OpenAI tool definitions without mutating the Synaptic tools.

---

### \_convert_tools() → None _(internal)_

Convert Synaptic [`Tool`](/api/core/tool) objects and global [`TOOL_REGISTRY`](/api/core/tool#object-properties) to OpenAI function definitions.

---
