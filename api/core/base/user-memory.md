---
title: User Memory
sidebar_position: 6
---

# UserMem

Specialized [Memory](/api/core/base/memory) subclass for user messages. Defaults role to `"user"`.

---

## Example

```python
from synaptic.core.base.memory import UserMem
from datetime import datetime

user_msg = UserMem("Hello!", created=datetime.now())
print(user_msg)
```

---

## Class hierarchy

```
Memory
 └── UserMem
```

---

## Info

- See also: [Memory](/api/core/base/memory), [History](/api/core/base/history)

---

## Constructor

### UserMem(message: str, created, role="user")

| Name      | Type                      | Description                 |
| --------- | ------------------------- | --------------------------- |
| `message` | **str**                   | Text content of the message |
| `created` | **datetime / any**        | Timestamp or marker         |
| `role`    | **str**, default `"user"` | Role of the speaker         |

---

## Object methods

### **repr**()

String representation of the memory object.

**`Returns:`** Formatted string of the memory object.

---
