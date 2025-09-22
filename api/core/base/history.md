---
title: History
sidebar_position: 8
---

# History

Conversation history manager. Stores a rolling window of [Memory](/api/core/base/memory) objects.

---

## Example

```python
from synaptic.core.base.memory import History, UserMem, ResponseMem
from datetime import datetime

history = History(size=5)
history.add(UserMem("Hello!", datetime.now()))
print(history.window(3))
```

---

## Class hierarchy

```
History
```

---

## Info

- See also: [Memory](/api/core/base/memory),
  [UserMem](/api/core/base/user-memory), [ResponseMem](/api/core/base/response-memory)

---

## Constructor

### History(memoryList: List[Memory] = [], size: int = 10)

| Name         | Type                                                  | Description                        |
| ------------ | ----------------------------------------------------- | ---------------------------------- |
| `memoryList` | **List\[[Memory](/api/core/base/memory)\]**, optional | Initial list of memory objects     |
| `size`       | **int**, default 10                                   | Maximum number of memories to keep |

---

## Object properties

| Property     | Type                                        | Description                    |
| ------------ | ------------------------------------------- | ------------------------------ |
| `MemoryList` | **List\[[Memory](/api/core/base/memory)\]** | Current list of memory objects |
| `size`       | **int**                                     | Maximum history length         |

---

## Object methods

### add(memory: [Memory](/api/core/base/memory)) → None

Add a memory object to the history and enforce size limit.

| Parameter | Type                                | Description             |
| --------- | ----------------------------------- | ----------------------- |
| `memory`  | **[Memory](/api/core/base/memory)** | Memory object to append |

**`Returns:`** None

---

### window(size: int) → list\[[Memory](/api/core/base/memory)\]

Modify and apply the history window size.

| Parameter | Type    | Description              |
| --------- | ------- | ------------------------ |
| `size`    | **int** | New maximum history size |

**`Returns:`** Updated memory list.

---

### _size_update() → None _(internal)\_

Ensure history does not exceed the defined size. Pops oldest memory if needed.

---
