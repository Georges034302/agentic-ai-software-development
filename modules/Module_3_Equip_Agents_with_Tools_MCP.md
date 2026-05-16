# Module 3 — Equip Agents with Tools (MCP)

> 💡 **Hands-on Labs:** For practical exercises that complement this module, see the [labs/](../labs) directory or start with [Lab 3: Equip Agents with Tools (MCP)](../labs/Lab_3_Equip_Agents_with_Tools_MCP.md).

> **Module goal.** Learn how to connect AI agents to real developer tools (IDEs, CLIs, APIs, code repositories) and invoke them safely and effectively using the Model Context Protocol (MCP).

> **Agentic AI Engineering Focus**
>
> This module is dedicated to practical integration: giving agents the ability to use real-world developer tools, automate workflows, and interact with codebases and APIs.

## Table of Contents

- [3.1 Integrating Agents with IDEs, CLIs, and Repos](#31-integrating-agents-with-ides-clis-and-repos)
- [3.2 Model Context Protocol (MCP) Basics](#32-model-context-protocol-mcp-basics)
- [3.3 Tool Registry and Invocation Patterns](#33-tool-registry-and-invocation-patterns)

---

## 3.1 Integrating Agents with IDEs, CLIs, and Repos

> **Agents become powerful when they can use the same tools as developers.**

**Common integrations:**
- IDE APIs (e.g., VS Code extensions)
- Command-line tools (e.g., git, pytest, docker)
- Code repository APIs (e.g., GitHub, GitLab)

**Example: Python agent running a CLI command**

```python
import subprocess

def run_tests():
	result = subprocess.run(["pytest", "--maxfail=1"], capture_output=True, text=True)
	print(result.stdout)
	return result.returncode == 0

# Agent can call run_tests() as part of its workflow
```

---

## 3.2 Model Context Protocol (MCP) Basics

> **MCP is a standard for exposing tools and APIs to agents in a structured, discoverable way.**

**Key ideas:**
- Each tool is described by a schema (name, parameters, output).
- Agents can discover, select, and invoke tools at runtime.
- MCP enables safe, auditable tool use (with logging, validation, and policy enforcement).

**Example: MCP tool schema (YAML)**

```yaml
name: run_tests
description: Run the project test suite using pytest
parameters:
  - name: maxfail
	type: integer
	default: 1
output:
  type: string
  description: Pytest output log
```

---

## 3.3 Tool Registry and Invocation Patterns

> **A tool registry is a catalog of all tools an agent can use.**

**Best practices:**
- Register only safe, well-documented tools.
- Validate all inputs and outputs.
- Log every tool invocation for audit and debugging.

**Example: Python tool registry and invocation**

```python
tool_registry = {
	"run_tests": run_tests,
	# ... other tools ...
}

def invoke_tool(tool_name, *args, **kwargs):
	if tool_name in tool_registry:
		return tool_registry[tool_name](*args, **kwargs)
	else:
		raise ValueError(f"Tool {tool_name} not found")

# Agent can call invoke_tool("run_tests")
```

---

## 🎯 Module 3 — Takeaways

1. **Agents gain real power by integrating with developer tools and APIs.**
2. **MCP provides a safe, structured way to expose tools to agents.**
3. **Tool registries and invocation patterns enable scalable, auditable automation.**

> ➡️ **Next:** [Module 4 — Constrain Agents Safely](Module_4_Constrain_Agents_Safely.md)

