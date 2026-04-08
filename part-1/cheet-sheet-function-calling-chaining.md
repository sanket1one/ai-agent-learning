# 🛠️ Foundations of Tool Calling and Chaining
> **Cheat Sheet** | Estimated Time: 20 minutes

## 1. Tool Calling Fundamentals
Tool calling enables chat models to respond to prompts by requesting the execution of specific functions. 

**Critical Concept:** The model **does not** execute the tool itself. It merely generates the **structured arguments** required. Running the tool (or choosing not to) is the responsibility of the application/user.

---

## 2. Tool Calling Workflow
The lifecycle of a tool-enabled request follows these specific steps:

| Step | Process | Explanation |
| :--- | :--- | :--- |
| **1** | **Setup & Query** | Provide tool definitions and your natural language question. |
| **2** | **Tool Selection** | The model identifies the required tool and outputs a structured request (e.g., `get_weather("Paris")`). |
| **3** | **Execution** | The application runs the Python function with the model's arguments. |
| **4** | **Result Passing** | The tool output (e.g., `{"temp": 14}`) is fed back into the model's memory. |
| **5** | **Final Response** | The model synthesizes the tool result into a natural language reply. |



---

## 3. LangChain Tool Creation Methods
All tools in LangChain are built upon the **`BaseTool`** blueprint.

### 🏗️ Method 1: Subclassing `BaseTool`
The most flexible method. Offers maximum control at the expense of more code.
* **Best for:** Custom instance variables, complex async methods, and bespoke behavior.

### 📦 Method 2: The `Tool` Class
Encapsulates a function with metadata (name, description). 
* **Note:** Primarily handles **single string inputs**. Used for backward compatibility.

### 🪄 Method 3: The `@tool` Decorator
The **recommended modern approach**. It automatically infers schema from function signatures and docstrings.
* **Result:** Creates a `StructuredTool` that handles complex, multi-argument inputs.

### 🔧 Method 4: `StructuredTool`
Modern foundation for tools with multiple inputs of arbitrary types. Supports complex Pydantic schemas.

---

## 4. Checking & Using Your Tools

### 🔍 1. Inspecting Tool Schema
Check what a tool expects before binding it:
```python
print(my_tool.name)
print(my_tool.description)
print(my_tool.args)