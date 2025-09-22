---
title: Gemini Adapter
sidebar_position: 14
---

# GeminiAdapter

Adapter for Google Gemini models. Handles conversion of Synaptic tools, history management, and content generation via the Gemini API.

---

## Example

```python
from synaptic.core.provider.gemini import GeminiAdapter
from synaptic.core.base.memory import History, ResponseFormat
from synaptic.core.tool import Tool
from datetime import datetime

history = History()
tools = [Tool(name="greet", declaration={"name": "greet", "description": "Greets a user", "parameters": {"type": "object", "properties": {"name": {"type": "string"}}, "required": ["name"]}})]

adapter = GeminiAdapter(
    model="gemini-1",
    history=history,
    api_key="YOUR_API_KEY",
    response_format=ResponseFormat.NONE,
    response_schema=None,
    temperature=0.7,
    tools=tools
)

response = adapter.invoke("Hello Gemini!")
print(response.message)
```

---

## Class hierarchy

```
BaseModel
 └── GeminiAdapter
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [History](/api/core/base/history), [ResponseMem](/api/core/base/response-memory), [Tool](/api/core/tool)

---

## Constructor

### GeminiAdapter(model: str, ...)

| Name              | Type                                                      | Description                                                      | Default |
| ----------------- | --------------------------------------------------------- | ---------------------------------------------------------------- | ------- |
| `model`           | **str**                                                   | Gemini model to use                                              | —       |
| `history`         | **[History](/api/core/base/history)**                     | Conversation history manager                                     | —       |
| `api_key`         | **str**                                                   | API key for Gemini                                               | —       |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Desired structured response format                               | —       |
| `response_schema` | **Any**                                                   | JSON schema for structured responses (if `JSON` response_format) | —       |
| `temperature`     | **float**                                                 | Sampling temperature                                             | 0.8     |
| `tools`           | **list\[[Tool](/api/core/tool)\]**, optional              | Synaptic tools to bind                                           | None    |

---

## Object properties

| Property          | Type                                                      | Description                             |
| ----------------- | --------------------------------------------------------- | --------------------------------------- |
| `client`          | **genai.Client**                                          | Gemini API client                       |
| `model`           | **str**                                                   | Name of the Gemini model                |
| `synaptic_tools`  | **list\[[Tool](/api/core/tool)\]**                        | Synaptic tools attached to this adapter |
| `gemini_tools`    | **list\[types.Tool\]**                                    | Converted Gemini tool objects           |
| `temperature`     | **float**                                                 | Sampling temperature                    |
| `history`         | **[History](/api/core/base/history)**                     | Conversation history                    |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Response format type                    |
| `response_schema` | **Any**                                                   | Schema for structured responses         |
| `role_map`        | **dict\[str,str\]**                                       | Maps Synaptic roles to Gemini roles     |

---

## Object methods

### invoke(prompt: str, ...) → [ResponseMem](/api/core/base/response-memory)

Generate a response using Gemini.

| Parameter  | Type    | Description                                    |
| ---------- | ------- | ---------------------------------------------- |
| `prompt`   | **str** | User or system message                         |
| `role`     | **str** | Must be `"user"`, `"assistant"`, or `"system"` |
| `**kwargs` | —       | Additional parameters for Gemini API call      |

**`Returns:`** **[ResponseMem](/api/core/base/response-memory)** object containing the assistant message and any tool calls.

---

### to_contents() → list\[types.Content\]

Convert conversation history to Gemini `Content` objects.

**`Returns:`** List of `types.Content` suitable for Gemini API input.

---

### \_invalidate_tools() _(internal)_

Update Gemini-side tools without mutating the Synaptic tools.
Used to auto update [tools](/api/core/tool) from [TOOL_REGISTRY](/api/core/tool#object-properties).

---

### \_convert_tools() → None _(internal)_

Convert Synaptic [`Tool`](/api/core/tool) objects and global [`TOOL_REGISTRY`](/api/core/tool#object-properties) to Gemini `types.Tool` objects.

---
