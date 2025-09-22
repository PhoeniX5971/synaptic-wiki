---
sidebar_position: 5
---

# Tools

We will now see how to use **tools** with the model.
Tools are external functions that the model can call to get more information or
perform actions.

We will need to:

1. Import `Tool` class.
2. Make a callable function.
3. Make a function declaration for the model.
4. Create a tool.
5. Bind the tool to the model.
6. Enable `autorun`.

## Manual Binding

:::note
We follow standard function calling declaration style.
:::

```py title="test.py" {1,6-7,10-21,23-28,35,44,46} showLineNumbers
from synaptic.core import Model, Provider, Tool
import os

api_key = os.getenv("GEMINI_API_KEY", "")

def add(a: int, b: int) -> int:
    return a + b


add_declaration = {
    "name": "add",
    "description": "Add two numbers together.",
    "parameters": {
        "type": "object",
        "properties": {
            "a": {"type": "integer", "description": "First number to add"},
            "b": {"type": "integer", "description": "Second number to add"},
        },
        "required": ["a", "b"],
    },
}

add_tool = Tool(
    name="add",
    declaration=add_declaration,
    function=add,
    default_params={"a": 0, "b": 0},
)

model = Model(
    provider=Provider.GEMINI,
    model="gemini-2.5-flash",
    api_key=api_key,
    automem=True,
    tools=[add_tool] # you can also use model.bind_tools([add_tool])
)

prompt = "Use the add tool to sum 12 and 30."

response = model.invoke(prompt)

print(response.message)
print("\n\n")
print(response.tool_calls)
print("\n\n")
print(response.tool_results)
print("\n\n")
print(model.history.MemoryList) # -> also saved in memory
```

```md title="Output"
[<ToolCall(name='add', args={ a=12, b=30 })>]

[{'name': 'add', 'result': 42}]

[<Memory role=assistant message='' created=2025-09-16 23:04:47.114534+00:00 tool_calls=[<ToolCall(name='add', args={ a=12, b=30 })>] tool_results=[{'name': 'add', 'result': 42}]>]
```

## Using Decorator

```py
from synaptic.core import autotool
@autotool(
    description="A tool that adds two numbers",
    param_descriptions={"a": "First integer", "b": "Second integer"},
)
def add_tool(a: int, b: int) -> int:
    return a + b
```

This will auto add the tool into the global tool registry and reload the tools
for the models.
