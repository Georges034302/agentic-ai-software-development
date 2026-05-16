# Module 2 — Drive Agents with Prompts & Specs

> 💡 **Hands-on Labs:** For practical exercises that complement this module, see the [labs/](../labs) directory or start with [Lab 2: Drive Agents with Prompts & Specs](../labs/Lab_2_Drive_Agents_with_Prompts_and_Specs.md).

> **Module goal.** Learn how to design, test, and iterate prompts that enable AI agents to generate, review, and refactor code effectively and safely.

> **Agentic AI Engineering Focus**
>
> This module is dedicated to prompt engineering for agentic AI in software development. You’ll learn how to craft prompts that drive reliable, auditable, and context-aware agent behavior—beyond simple chat or code-completion.

## Table of Contents

- [2.1 Principles of Effective Prompt Engineering](#21-principles-of-effective-prompt-engineering)
- [2.2 Backend-Specific Prompt Patterns](#22-backend-specific-prompt-patterns)
- [2.3 Prompt Testing and Iteration](#23-prompt-testing-and-iteration)

---

## 2.1 Principles of Effective Prompt Engineering

> **Prompt engineering is the art and science of getting the right output from an AI agent—every time.**

**Key principles:**

- **Be explicit.** State the agent’s role, the task, and the output format.
- **Provide context.** Include relevant code, requirements, or examples.
- **Constrain output.** Use schemas, templates, or clear instructions for structure.
- **Anticipate failure.** Tell the agent what to do if it’s unsure or encounters errors.

**Example: Prompt for Code Refactoring**

```text
You are a senior Python developer. Refactor the following function for readability and maintainability. Do not change its behavior. Return only the refactored code.

def process(data):
	# ... complex logic ...
	return result
```

**Example: Prompt for Code Review**

```text
You are a code reviewer. Review the following pull request diff for security, style, and correctness. List any issues found and suggest improvements.

--- DIFF START ---
...diff here...
--- DIFF END ---
```

---

## 2.2 Backend-Specific Prompt Patterns

Different LLM backends (e.g., Anthropic Claude, AWS Kiro) may require tailored prompt patterns for best results.

**Claude Pattern Example:**

```text
Human: You are an expert Python engineer. Given the code below, refactor it for clarity and add type hints. Output only the improved code.

def add(a, b):
	return a + b

Assistant:
```

**Kiro Pattern Example:**

```json
{
  "role": "engineer",
  "task": "refactor",
  "language": "python",
  "instructions": "Improve readability and add docstrings. Output only the refactored code.",
  "code": "def multiply(x, y):\n    return x * y"
}
```

**Tips:**
- Use the backend’s preferred structure (e.g., Human/Assistant for Claude, JSON for Kiro).
- Always specify the output format and constraints.
- Include examples or test cases if possible.

---

## 2.3 Prompt Testing and Iteration

> **Prompt engineering is iterative.** Test, evaluate, and refine prompts to ensure reliability and safety.

**Testing strategies:**
- Try prompts on multiple code samples and edge cases.
- Check for hallucinations, unsafe changes, or missing requirements.
- Use automated tests to validate agent output.

**Example: Python Test Harness for Prompt Evaluation**

```python
# Example: Testing an agent's code refactor output
import openai  # or anthropic, boto3 for Kiro, etc.

def test_prompt(prompt, code, expected_substring):
	# This is a placeholder for actual LLM API call
	response = call_llm_api(prompt.replace("<CODE>", code))
	assert expected_substring in response, "Refactor did not include expected change."

prompt = "You are a senior Python developer. Refactor the following code to use list comprehensions. Return only the refactored code.\n<CODE>"
code = "def squares(nums):\n    result = []\n    for n in nums:\n        result.append(n*n)\n    return result"
expected = "return [n*n for n in nums]"
test_prompt(prompt, code, expected)
```

**Iteration:**
- Adjust instructions, add examples, or clarify constraints based on test results.
- Document prompt versions and what works best for your backend and use case.

---

## 🎯 Module 2 — Takeaways

1. **Explicit, context-rich prompts yield better agent output.**
2. **Prompt patterns should be tailored to your backend (Claude, Kiro, etc.).**
3. **Testing and iteration are essential for reliable, safe agent behavior.**

> ➡️ **Next:** [Module 3 — Equip Agents with Tools (MCP)](Module_3_Equip_Agents_with_Tools_MCP.md)

