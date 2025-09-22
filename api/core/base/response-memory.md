---
title: Response Memory
sidebar_position: 7
---

# ResponseMem

Specialized [Memory](/api/core/base/memory) subclass for assistant responses. Includes tool calls and results.

---

## Example

```python
from synaptic.core.base.memory import ResponseMem
from synaptic.core.tool import ToolCall
from datetime import datetime

response = ResponseMem(
    message="Hi there!",
    created=datetime.now(),
    tool_calls=[ToolCall(name="greet", args={"name": "Alice"})],
    tool_results=[]
)
print(response.list_tool_calls())
```

---

## Class hierarchy

```
Memory
 └── ResponseMem
```

---

## Info

- See also: [Memory](/api/core/base/memory), [ToolCall](/api/core/tool-call)

---

## Constructor

### ResponseMem(message: str, ...)

| Name           | Type                           | Description                  |
| -------------- | ------------------------------ | ---------------------------- |
| `message`      | **str**                        | Text content of the response |
| `created`      | **datetime / any**             | Timestamp or marker          |
| `tool_calls`   | **List[ToolCall]**             | Tools invoked by the model   |
| `tool_results` | **list**, optional             | Results of tool executions   |
| `role`         | **str**, default `"assistant"` | Role of the speaker          |

---

## Object methods

### list_tool_calls() → List\[str\]

Get the names of all tools called by the assistant.

**`Returns:`** List of tool names.

---

### get_tool_call(name: str) → [ToolCall](/api/core/tool-call)

Retrieve the first tool call matching the given name. Raises `IndexError` if not found.

| Parameter | Type    | Description      |
| --------- | ------- | ---------------- |
| `name`    | **str** | Name of the tool |

**`Returns:`** **[ToolCall](/api/core/tool-call)**
