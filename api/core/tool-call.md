---
title: Tool Call
sidebar_position: 12
---

# ToolCall

Represents a call to a specific tool with arguments in Synaptic.

---

## Example

```python
from synaptic.core.tool import ToolCall

# Create a ToolCall instance
call = ToolCall(
    name="greet",
    args={"name": "Alice"}
)

# Access argument
print(call.get_arg("name"))  # Output: Alice

# List all argument keys
print(list(call.list_args()))  # Output: ["name"]
```

---

## Class hierarchy

```
ToolCall
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [Tool](/api/core/tool), [TOOL_REGISTRY](/api/core/tool#object-properties)

---

## Constructors

### ToolCall(name: str, args: dict)

Create a new tool call.

| Name   | Type     | Description                   |
| ------ | -------- | ----------------------------- |
| `name` | **str**  | Name of the tool being called |
| `args` | **dict** | Arguments for the tool        |

---

## Object properties

| Property | Type     | Description                    |
| -------- | -------- | ------------------------------ |
| `name`   | **str**  | Name of the tool being called  |
| `args`   | **dict** | Arguments provided to the tool |

---

## Object methods

### get_arg(key: str) → Any

Retrieve a specific argument from the tool call.

| Parameter | Type    | Description   |
| --------- | ------- | ------------- |
| `key`     | **str** | Argument name |

**`Returns:`** Value of the argument.

---

### list_args() → Iterable

List all argument keys.

**`Returns:`** Iterable of argument names.

---

### **repr**() → str

Get a string representation of the tool call.

**`Returns:`** String in the format:

```
<ToolCall(name='tool_name', args={ key1=value1, key2=value2, ... })>
```
