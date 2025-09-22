---
title: Memory
sidebar_position: 5
---

# Memory

Base memory object for storing a single conversational turn in Synaptic.

---

## Example

```python
from synaptic.core.base.memory import Memory
from datetime import datetime

memory = Memory(message="Hello!", created=datetime.now(), role="user")
print(memory)
```

---

## Class hierarchy

```
Memory
```

---

## Info

- Copyright: 2025 Synaptic contributors
- Authors: Phoenix
- See also: [ResponseMem](/api/core/base/response-memory),
  [UserMem](/api/core/base/user-memory), [History](his)

---

## Constructor

### Memory(message: str, created, role: str)

| Name      | Type               | Description                                              |
| --------- | ------------------ | -------------------------------------------------------- |
| `message` | **str**            | Text content of the memory                               |
| `created` | **datetime / any** | Timestamp or marker for creation                         |
| `role`    | **str**            | Role of the speaker: `"user"`, `"assistant"`, `"system"` |

---

## Object methods

### **repr**()

String representation of the memory object.

**`Returns:`** Formatted string of the memory object.

---
