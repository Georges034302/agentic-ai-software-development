# Module 5 — Multi-Agent Workflows in Software Projects

> 💡 **Hands-on Labs:** For practical exercises that complement this module, see the [labs/](../labs) directory or start with [Lab 5: Multi-Agent Workflows in Software Projects](../labs/Lab_5_Multi_Agent_Workflows_in_Software_Projects.md).

> **Module goal.** Learn how to design, implement, and orchestrate multi-agent workflows for complex software engineering tasks.

> **Agentic AI Engineering Focus**
>
> This module is about collaboration: enabling multiple agents to coordinate, communicate, and deliver outcomes together.

## Table of Contents

- [5.1 Supervisor/Worker and Peer-to-Peer Patterns](#51-supervisorworker-and-peer-to-peer-patterns)
- [5.2 Communication and Coordination](#52-communication-and-coordination)
- [5.3 Workflow Orchestration](#53-workflow-orchestration)
- [5.4 Backend-Specific Workflow Examples](#54-backend-specific-workflow-examples)

---

## 5.1 Supervisor/Worker and Peer-to-Peer Patterns

> **Multi-agent systems can split work, specialize, and collaborate for greater impact.**

**Patterns:**
- Supervisor/worker (one agent plans, others execute)
- Peer-to-peer (agents negotiate or share tasks)

**Example: Python supervisor/worker agents**

```python
class WorkerAgent:
	def __init__(self, name):
		self.name = name
	def do_task(self, task):
		print(f"{self.name} working on: {task}")
		return f"{task} done"

class SupervisorAgent:
	def __init__(self, workers):
		self.workers = workers
	def assign_tasks(self, tasks):
		results = []
		for worker, task in zip(self.workers, tasks):
			results.append(worker.do_task(task))
		return results

# Usage
workers = [WorkerAgent("Alice"), WorkerAgent("Bob")]
supervisor = SupervisorAgent(workers)
print(supervisor.assign_tasks(["Write tests", "Refactor code"]))
```

---

## 5.2 Communication and Coordination

> **Agents need protocols to share information, negotiate, and synchronize.**

**Techniques:**
- Shared memory (database, message queue)
- Explicit messaging (APIs, events)

**Example: Simple message passing**

```python
class MessageBus:
	def __init__(self):
		self.messages = []
	def send(self, sender, recipient, content):
		self.messages.append((sender, recipient, content))
	def receive(self, recipient):
		return [msg for msg in self.messages if msg[1] == recipient]

# Usage
bus = MessageBus()
bus.send("Supervisor", "Alice", "Please review PR #42")
print(bus.receive("Alice"))
```

---

## 5.3 Workflow Orchestration

> **Orchestration coordinates agents, tools, and data to deliver business outcomes.**

**Patterns:**
- Sequential pipeline
- Parallel fan-out/fan-in
- Plan-and-execute

**Example: Sequential pipeline**

```python
def pipeline(steps, input_data):
	data = input_data
	for step in steps:
		data = step(data)
	return data

# Usage
def step1(data): return data + " step1"
def step2(data): return data + " step2"
print(pipeline([step1, step2], "start"))
```

---

## 5.4 Backend-Specific Workflow Examples

> **Different agent backends may have unique orchestration features.**

**Claude:**
- Supports tool use, function calling, and multi-turn planning.

**Kiro:**
- Supports workflow templates, event-driven triggers, and policy enforcement.

---

## 🎯 Module 5 — Takeaways

1. **Multi-agent workflows enable specialization, parallelism, and resilience.**
2. **Communication and orchestration are key to complex automation.**
3. **Choose patterns and backends that fit your engineering needs.**

> ➡️ **Next:** [Module 6 — Agentic RAG for Codebases](Module_6_Agentic_RAG_for_Codebases.md)

