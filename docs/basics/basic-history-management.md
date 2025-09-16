---
sidebar_position: 4
---

# Basic History Management

We will now use the built-in history management of Synaptic.

## Using Auto Memory

We will need to enable **`automem`**.

```py title="test.py" {10,23} showLineNumbers
from synaptic.core import Model, Provider
import os

api_key = os.getenv("GEMINI_API_KEY", "")

model = Model(
    provider=Provider.GEMINI,
    model="gemini-2.5-flash",
    api_key=api_key,
    automem=True,
)

prompt = (
    "You are japanese pop fan."
    "Tell me what do you think about Ado, the japanese idol."
    "Keep it real short."
)

response = model.invoke(prompt)

print(response.message)
print("\n\n")
print(model.history.MemoryList)
```

```md title="Output"
Absolute vocal powerhouse, totally captivating and unique. Love her style and the mystery!



[<Memory role=assistant message='Absolute vocal powerhouse, totally captivating and unique. Love her style and the mystery!' created=2025-09-16 22:37:57.166735+00:00 tool_calls=[] tool_results=[]>]
```

## More on History

**`History`** class is used to manage the basic memory of the model.

### Key Attributes

- `MemoryList`: List of memories.
- `size`: Limit of window.

### Key Methods

- `add(memory: Memory)`: add a memory to the memory list.
- `window(size: int)`: update the window size.

:::note
If you are using `automem` is true, you don't need to manually add memories, as
they are added automatically.
:::
