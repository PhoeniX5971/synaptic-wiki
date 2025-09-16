---
sidebar_position: 2
---

# Basic Usage

Start by creating an empty python file.

## Imports


```py title="test.py" {1-2} showLineNumbers
from synaptic import Model, Provider
import os
```

We import a `model` and a `provider`.
The `model` is the universal LLM, and the `provider` is the `enum provider`.
We will also import `os` to access environment variables.

## Basic Initialization

```py title="test.py" {4,6-10} showLineNumbers
from synaptic.core import Model, Provider
import os

api_key = os.getenv("GEMINI_API_KEY", "")

model = Model(
    provider=Provider.GEMINI,
    model="gemini-2.5-flash",
    api_key=api_key,
)
```

## Basic Call

```py title="test.py" {12-16,18,20} showLineNumbers
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
```

```md title="Output"
Ado?
Mind-blowing vocal powerhouse!
Not a typical "idol" but a unique, phenomenal artist.
Obsessed with her energy!
```
