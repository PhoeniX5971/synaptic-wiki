---
title: Core Model
sidebar_position: 9
---

# Core Model

Universal model which allows usage of different LLM providers.

---

## Example

```python
from synaptic.core.model import Model
from synaptic.core.provider import Provider

model = Model(
    provider=Provider.OPENAI,
    model="gpt-4",
    api_key="sk-...",
    temperature=0.7,
    max_tokens=2048,
    autorun=True,
    automem=True,
)
```

---

## Class hierarchy

```
BaseModel
   └── Model
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [Provider](/api/core/provider), [Tool](/api/core/tool), [History](/api/core/base/memory#history)

---

## Constructor

### Model(...)

Create a new universal model.

| Name              | Type                                                      | Description                      | Default         |
| ----------------- | --------------------------------------------------------- | -------------------------------- | --------------- |
| `provider`        | **[Provider](/api/core/provider)**                        | Enum: select LLM provider        | `GEMINI`        |
| `model`           | **str**                                                   | Model to use                     | —               |
| `temperature`     | **float**                                                 | Sampling temperature             | `0.8`           |
| `api_key`         | **str**                                                   | API key for the provider         | required        |
| `max_tokens`      | **int**                                                   | Maximum tokens for the response  | `1024`          |
| `tools`           | **List[[Tool](/api/core/tool)]**                          | Tools to bind to the model       | `None`          |
| `history`         | **[History](/api/core/base/memory#history)**              | Conversation history manager     | new `History()` |
| `autorun`         | **bool**                                                  | Automatically run returned tools | `False`         |
| `automem`         | **bool**                                                  | Automatically store interactions | `False`         |
| `blacklist`       | **List[str]**                                             | Tools to ignore on autorun       | `[]`            |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Structured response format       | `NONE`          |
| `response_schema` | **Any**                                                   | Structured response schema       | `None`          |

---

## Object properties

| Property          | Type                                                      | Description                                   |
| ----------------- | --------------------------------------------------------- | --------------------------------------------- |
| `provider`        | **[Provider](/api/core/provider)**                        | Selected LLM provider                         |
| `model`           | **str**                                                   | Model name                                    |
| `temperature`     | **float**                                                 | Sampling temperature                          |
| `api_key`         | **str**                                                   | API key                                       |
| `max_tokens`      | **int**                                                   | Token budget per request                      |
| `tools`           | **List[[Tool](/api/core/tool)]**                          | Bound tools                                   |
| `history`         | **[History](/api/core/base/memory#history)**              | Conversation history (if `automem=True`)      |
| `autorun`         | **bool**                                                  | Whether tools are executed automatically      |
| `automem`         | **bool**                                                  | Whether interactions are stored automatically |
| `blacklist`       | **List[str]**                                             | Blacklisted tool names                        |
| `response_format` | **[ResponseFormat](/api/core/base/model#responseformat)** | Desired response format                       |
| `response_schema` | **Any**                                                   | Schema used for structured responses          |

---

## Object methods

- ### bind_tools(tools: List[[Tool](/api/core/tool)]) → None

Bind additional tools to the model.

| Parameter | Type                              | Description                |
| --------- | --------------------------------- | -------------------------- |
| `tools`   | **List\[[Tool](/api/core/tool)]** | Tools to bind to the model |

**`Returns:`** None

- ### invoke(prompt: str, ...) → [ResponseMem](/api/core/base/memory#responsemem)

Invoke the model with a prompt.

| Parameter | Type               | Description                                    |
| --------- | ------------------ | ---------------------------------------------- |
| `prompt`  | **str**            | User/system/assistant message                  |
| `role`    | **str**            | Must be `"user"`, `"assistant"`, or `"system"` |
| `autorun` | **bool**, optional | Override for automatic tool execution          |
| `automem` | **bool**, optional | Override for automatic memory storage          |

**`Returns`**: **[ResponseMem](/api/core/base/mem#responsemem)**

---

## Internal methods

_(not typically needed in external usage, but documented for completeness)_

- `_initiate_model() → Any`  
   Initialize adapter for provider.
- `_run_tools(tool_calls: List[ToolCall]) → List[Any]`  
   Run tool calls if autorun is enabled.

---
