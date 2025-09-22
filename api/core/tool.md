---
title: Tool
sidebar_position: 11
---

# Tool

Structured support for defining, registering, and invoking tools in Synaptic.

---

## Example

```python
from synaptic.core.tool import Tool, autotool

# Define a tool manually
def greet(name: str):
    return f"Hello, {name}!"

tool = Tool(
    name="greet",
    declaration={
        "name": "greet",
        "description": "Greets a user by name",
        "parameters": {"type": "object", "properties": {"name": {"type": "string"}}, "required": ["name"]},
    },
    function=greet,
)

# Using the autotool decorator
@autotool(description="Adds two numbers")
def add(a: int, b: int):
    return a + b
```

---

## Class hierarchy

```
Tool
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [Model](/api/core/model), [Provider](/api/core/provider), [ToolCall](/api/core/tool-call),
  [History](/api/core/base/memory#History), [autotool](/api/core/tool#-autotooldescription-str-----tool)

---

## Constructor

### Tool(...)

Create a new tool.

| Name              | Type                   | Description                                      | Default        |
| ----------------- | ---------------------- | ------------------------------------------------ | -------------- |
| `name`            | **str**                | Name of the tool                                 | —              |
| `declaration`     | **dict**               | Metadata about the tool                          | —              |
| `function`        | **Callable[..., Any]** | Function executed when the tool runs             | `lambda: None` |
| `default_params`  | **dict**, optional     | Default parameters                               | `{}`           |
| `add_to_registry` | **bool**               | Automatically register tool in **TOOL_REGISTRY** | `True`         |

---

## Object properties

| Property              | Type                   | Description                                         |
| --------------------- | ---------------------- | --------------------------------------------------- |
| `name`                | **str**                | Tool name                                           |
| `declaration`         | **dict**               | Tool metadata, including parameters and description |
| `function`            | **Callable[..., Any]** | Function executed by the tool                       |
| `default_params`      | **dict**               | Default parameters applied when run                 |
| **TOOL_REGISTRY**     | **dict**               | Global registry of tools                            |
| `_registry_callbacks` | **list**               | Functions called when the registry changes          |

---

## Object methods

### run(\*\*kwargs) → Any

Execute the tool with merged default and runtime parameters.

| Parameter  | Type | Description                             |
| ---------- | ---- | --------------------------------------- |
| `**kwargs` | —    | Runtime parameters to override defaults |

**`Returns:`** Result of the tool function.

---

## Decorators

### autotool(description: str = "", ...) → [Tool](/api/core/tool)

Automatically create a **Tool** from a Python function.

| Parameter            | Type                           | Description                                          |
| -------------------- | ------------------------------ | ---------------------------------------------------- |
| `description`        | **str**                        | Human-readable description of the tool               |
| `param_descriptions` | **dict\[str, str\]**, optional | Parameter → description mapping                      |
| `default_params`     | **dict**, optional             | Default parameters for the tool                      |
| `autobind`           | **bool**, default `True`       | Automatically register the tool in **TOOL_REGISTRY** |

**Usage:**

```python
@autotool(description="Adds two numbers")
def add(a: int, b: int):
    return a + b
```

**`Returns:`** **[Tool](/api/core/tool)**

## **Global methods**

These methods are part of the **Tool system**, allowing models to subscribe to changes in the global tool registry.

---

### registr_callback(fn: Callable[[], None])

Subscribe a [model](/api/core/model) (or any callable) to **tool registry changes**. Whenever the [`TOOL_REGISTRY`](/api/core/tool#object-properties) changes, all subscribed callbacks are invoked.

| Parameter | Type                   | Description                                        |
| --------- | ---------------------- | -------------------------------------------------- |
| `fn`      | **Callable[[], None]** | Function with no arguments to be called on updates |

**`Returns:`** None

> Use this to automatically update models or systems when tools are added, removed, or changed.
> If using the current providers, no need to touch this, it's built-in and will reload your tools on registry.

---

### \_notify*change() → None *(internal)\_

Calls all subscribed callbacks to notify them of a change in the tool registry.

**`Returns:`** None

> This is an **internal method** used by the [Tool](/api/core/tool) system when tools are added or modified. Do **not** call this directly in most use cases.

---
