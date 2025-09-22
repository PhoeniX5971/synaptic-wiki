---
sidebar_position: 6
---

# Structured Output

Simply set response_format to JSON and provide a pydantic schema.

```py

from synaptic.core import Model, Provider
from synaptic.core.base import ResponseFormat
from pydantic import BaseModel
from typing import List


class Response(BaseModel):
    message: str
    explanation: List[str]

model = Model(
    provider=Provider.GEMINI,
    model="gemini-2.5-flash",
    temperature=1,
    api_key=api_key,
    automem=True,
    response_format=ResponseFormat.JSON,
    response_schema=Response,
)
```

Output will be in response.message
