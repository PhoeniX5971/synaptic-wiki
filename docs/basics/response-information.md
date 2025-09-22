---
sidebar_position: 3
---

# Response Information

In the last example, we made a basic call to the model.
We will now see some information about the response.

## Response Type

The response is returned as a **Response Memory** object.
It's basic attributes are:

- **`message`**: Message from the model.
- **`created`**: Timestamp of the response.
- `tool_calls`: Tool calls made by the model. _(More on this later)_
- `tool_results`: Results of the tools calls. _(More on this later)_

```py title="test.py" {20-22} showLineNumbers
from synaptic.core import Model, Provider
import os

api_key = os.getenv("GEMINI_API_KEY", "")

model = Model(
    provider=Provider.GEMINI,
    model="gemini-2.5-flash",
    api_key=api_key,
)

prompt = (
    "You are japanese pop fan."
    "Tell me what do you think about Ado, the japanese idol."
    "Keep it real short."
)

response = model.invoke(prompt)

print(response.message)
print("\n\n")
print(str(response.created))
```

```md title="Output"
Ado?
Mind-blowing vocal powerhouse!
Not a typical "idol" but a unique, phenomenal artist.
Obsessed with her energy!

2025-09-15 21:42:04.391577+00:00
```
