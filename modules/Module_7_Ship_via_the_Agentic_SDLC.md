# Module 7 — AI-Augmented Software Engineering

> 💡 **Hands-on Labs:** For practical exercises that complement this module, see the [labs/](../labs) directory or start with [Lab 7: AI-Augmented Software Engineering](../labs/Lab_7_AI_Augmented_Software_Engineering.md).

> **Module goal.** Learn how to use agents for automated code reading, patch proposal, test automation, and to simulate PRs and reviews in the software development lifecycle.

> **Agentic AI Engineering Focus**
>
> This module is about practical AI augmentation of the SDLC: using agents to automate, review, and improve code safely and efficiently.

## Table of Contents

- [7.1 Code Reading, Patch Proposal, and Test Automation](#71-code-reading-patch-proposal-and-test-automation)
- [7.2 Simulating Pull Requests and Code Reviews](#72-simulating-pull-requests-and-code-reviews)
- [7.3 Best Practices for AI-in-the-Loop Development](#73-best-practices-for-ai-in-the-loop-development)

---

## 7.1 Code Reading, Patch Proposal, and Test Automation

> **Agents can automate code analysis, propose patches, and run tests.**

**Example: Automated code patch and test**

```python
import difflib

def propose_patch(original, refactored):
	diff = difflib.unified_diff(
		original.splitlines(),
		refactored.splitlines(),
		fromfile='original.py',
		tofile='refactored.py',
		lineterm=''
	)
	return '\n'.join(diff)

# Usage
original = "def add(a, b):\n    return a+b"
refactored = "def add(a: int, b: int) -> int:\n    return a + b"
print(propose_patch(original, refactored))
```

---

## 7.2 Simulating Pull Requests and Code Reviews

> **Agents can open PRs, review code, and even merge changes.**

**Example: Simulated PR creation (pseudo-code)**

```python
def open_pull_request(branch, title, description):
	# This would call the GitHub/GitLab API in a real agent
	print(f"Opened PR on {branch}: {title}\n{description}")

def review_code(diff):
	# Simulate a code review
	if "eval(" in diff:
		return "Security issue: avoid eval()"
	return "Looks good!"

# Usage
open_pull_request("feature/refactor", "Refactor add()", "Improved type hints.")
print(review_code("- return eval(expr)"))
```

---

## 7.3 Best Practices for AI-in-the-Loop Development

> **AI-in-the-loop means humans and agents collaborate for quality and safety.**

**Best practices:**
- Always review agent-generated code before merging
- Use automated tests and linters as gatekeepers
- Log all agent actions for traceability

**Example: Human-in-the-loop approval**

```python
def human_approval(change):
	print(f"Approve this change?\n{change}")
	return input("Type 'yes' to approve: ") == 'yes'

# Usage
if human_approval("Refactor add() to use type hints"):
	print("Change approved and merged.")
else:
	print("Change rejected.")
```

---

## 🎯 Module 7 — Takeaways

1. **Agents can automate code reading, patching, and testing.**
2. **Simulated PRs and reviews enable safe, scalable code changes.**
3. **AI-in-the-loop ensures quality, safety, and compliance.**

> ➡️ **Next:** [Module 8 — Productionizing Agentic Systems](Module_8_Productionizing_Agentic_Systems.md)

