---
title: Base Model
sidebar_position: 4
---

# BaseModel

Abstract base class for all models in Synaptic. Defines the interface for model invocation and response handling.

---

## Example

```python
from synaptic.core.base import BaseModel, ResponseMem
from synaptic.core.model import Model

# BaseModel cannot be instantiated directly
# Concrete classes like Model implement the invoke method
class MyModel(BaseModel):
    def invoke(self, prompt: str, **kwargs) -> ResponseMem:
        return ResponseMem(content=f"Echo: {prompt}")
```

:::danger
This class might get deprecated in future releases. Use **[Model](/api/core/model)** instead.
:::

---

## Class hierarchy

```
ABC
 └── BaseModel
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [Model](/api/core/model), [ResponseMem](/api/core/base/response-memory)

---

## Enums

### ResponseFormat

Defines the structured response formats for models.

| Name   | Value    | Description                     |
| ------ | -------- | ------------------------------- |
| `JSON` | `"json"` | Return responses in JSON format |
| `NONE` | `"none"` | No structured format applied    |

---

## Constructors

### BaseModel(...)

Abstract base class; cannot be instantiated directly.

| Name | Type | Description                              |
| ---- | ---- | ---------------------------------------- |
| —    | —    | Base class for all model implementations |

---

## Object methods

### invoke(prompt: str, \*\*kwargs) → ResponseMem

Abstract method to invoke the model with a prompt. Must be implemented by subclasses.

| Parameter  | Type    | Description                       |
| ---------- | ------- | --------------------------------- |
| `prompt`   | **str** | User/system/assistant message     |
| `**kwargs` | —       | Optional parameters for the model |

**`Returns:`** **ResponseMem**

---

## Notes

- Subclasses like **[Model](/api/core/model)** implement the `invoke` method.
- Use **[ResponseFormat](/api/core/base/model#responseformat)** to control structured response output.

---
