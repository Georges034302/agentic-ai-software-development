# Module 4 — Stateful and Guardrailed Agents

> 💡 **Hands-on Labs:** For practical exercises that complement this module, see the [labs/](../labs) directory or start with [Lab 4: Stateful and Guardrailed Agents](../labs/Lab_4_Stateful_and_Guardrailed_Agents.md).

> **Module goal.** Learn how to give agents memory, enforce safety and compliance with guardrails, and implement logging and observability for real-world use.

> **Agentic AI Engineering Focus**
>
> This module is about making agents robust, safe, and auditable—critical for production and enterprise use.

## Table of Contents

- [4.1 Memory and Session Management](#41-memory-and-session-management)
- [4.2 Guardrails for Safe Code Generation](#42-guardrails-for-safe-code-generation)
- [4.3 Logging, Observability, and Audit Trails](#43-logging-observability-and-audit-trails)

---

## 4.1 Memory and Session Management

> **Memory lets agents learn from the past and maintain context across steps.**

**Types of memory:**
- Short-term (within a session)
- Long-term (across sessions or tasks)

**Example: Simple Python memory for an agent**

```python
class AgentMemory:
	def __init__(self):
		self.history = []

	def remember(self, event):
		self.history.append(event)

	def recall(self):
		return self.history[-5:]  # Last 5 events

# Usage
memory = AgentMemory()
memory.remember("Ran tests: PASS")
print(memory.recall())
```

---

## 4.2 Guardrails for Safe Code Generation

> **Guardrails are rules and checks that keep agents safe, compliant, and reliable.**

**Common guardrails:**
- Output validation (schemas, regex, linters)
- Policy enforcement (no secrets, no destructive actions)
- Human-in-the-loop for high-impact changes

**Example: Python output validation guardrail**

```python
import re

def validate_code_output(code):
	# Example: Ensure no 'os.system' calls for safety
	if re.search(r'os\.system', code):
		raise ValueError("Unsafe code detected!")
	return True

# Usage
try:
	validate_code_output("import os\nos.system('rm -rf /')")
except ValueError as e:
	print(e)
```

---

## 4.3 Logging, Observability, and Audit Trails

> **Observability means you can see what the agent did, when, and why.**

**Best practices:**
- Log every action, tool call, and decision
- Store logs in a searchable, queryable format
- Enable audit trails for compliance

**Example: Simple logging in Python**

```python
import logging

logging.basicConfig(filename='agent.log', level=logging.INFO)

def agent_action(action):
	logging.info(f"Agent action: {action}")

# Usage
agent_action("Refactored function X")
```

---

## 🎯 Module 4 — Takeaways

1. **Memory and session management enable context-aware, adaptive agents.**
2. **Guardrails are essential for safety, compliance, and reliability.**
3. **Logging and observability make agents auditable and production-ready.**

> ➡️ **Next:** [Module 5 — Multi-Agent Workflows in Software Projects](Module_5_Multi_Agent_Workflows_in_Software_Projects.md)

