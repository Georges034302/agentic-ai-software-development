# Module 1 — Introduction to Agentic AI for Software Development

> 💡 **Hands-on Lab:** This module is paired with [Lab 1: Agentic AI for Software Development](../labs/Lab_1_Introduction_to_Agentic_AI_for_Software_Development.md), where you build a working *plan → act → observe → adapt* coding agent that writes and runs unit tests for a Python module.

> **Module goal.** Build a precise mental model of what agentic AI *is* in the context of **software development**, what makes it different from earlier AI coding tools, and where it creates measurable value across the engineering lifecycle.

> **Course focus.** This course is about **engineering agentic AI systems for software development** — autonomous, goal-driven agents that read code, edit code, run tools (tests, linters, build systems, VCS), observe results, and adapt. It is not about general LLM usage, image generation, or non-engineering chat assistants.

## Table of Contents

- [1.1 What is Agentic AI?](#11-what-is-agentic-ai)
- [1.2 Why Agentic AI for Software Engineering?](#12-why-agentic-ai-for-software-engineering)
- [1.3 Key Concepts and Terminology](#13-key-concepts-and-terminology)
- [1.4 From Module to Lab — Your First Coding Agent](#14-from-module-to-lab--your-first-coding-agent)

---

## 1.1 What is Agentic AI?

> **Agentic AI moves software from *answering questions* to *completing engineering work*.**
>
> A foundation model alone is a function: text in, text out. An **agent** wraps that function in a *loop*, gives it *tools* (file I/O, shells, test runners, VCS), gives it *memory*, and points it at a *goal* (e.g., "add unit tests for `add()` and `subtract()`"). The result is a system that can **plan, act, observe, and adapt — autonomously**.

### The Agent Loop

```
        ┌───────────────────┐
        │       GOAL        │   "Add unit tests for app.py"
        └─────────┬─────────┘
                  ▼
   ┌──────────────────────────────┐
   │  PLAN  →  ACT  →  OBSERVE    │  ← repeat until done / max retries
   │           ▲          │       │
   │           └── ADAPT ─┘       │
   └──────────────┬───────────────┘
                  ▼
        ┌───────────────────┐
        │      OUTCOME      │   test_app.py written, `unittest` reports OK
        └───────────────────┘
```

| Phase | What the coding agent does |
|---|---|
| **Plan** | Decompose the goal into ordered steps (e.g., "write `test_app.py`", "run `python -m unittest`", "verify exit code 0"). |
| **Act** | Use a *tool* — write a file, run a shell command, call a Git API, edit code. |
| **Observe** | Read the actual result (stdout, exit code, file diff, lint warnings). |
| **Adapt** | If the observation indicates failure, revise the plan or fix the artifact and retry. |

### Where it sits on the AI-coding spectrum

| Tool generation | Trigger | Output | Autonomy |
|---|---|---|---|
| **Autocomplete** (e.g., classic IntelliSense) | Keystroke | Token suggestions | None — you accept/reject each char |
| **Chat assistant** (a coding chatbot) | Question | Code snippet in a reply | Low — you copy/paste/run manually |
| **AI pair programmer** (inline LLM) | Edit context | Multi-line completions, refactors on demand | Medium — bounded to the open buffer |
| **Agentic AI for software dev** *(this course)* | A **goal** | Files written, tests run, PRs opened, errors fixed | **High — closes the loop on real artifacts** |

### Anatomy of a coding agent

A working agent has five engineering surfaces — every later module in this course adds depth to one of them:

| Component | Role in software development | Covered in |
|---|---|---|
| **Goal / prompt contract** | Unambiguous task statement + success criteria. | Module 2 |
| **Tools** | File system, shell, test runner, linter, Git, IDE/MCP. | Module 3 |
| **Memory** | Files read, decisions made, prior errors, repo facts. | Module 4 |
| **Guardrails** | What the agent may *not* touch; how output is validated. | Module 4 |
| **Loop / control** | The plan→act→observe→adapt driver and stop conditions. | Module 1 (here) + Module 5 |

### Concrete example — a unit-test agent (Lab 1 preview)

> **Goal:** *"Add unit tests for `add()` and `subtract()` in `backend_app/app.py`."*

1. **Plan** — `["write backend_app/test_app.py", "run python -m unittest", "verify all tests pass"]`
2. **Act** — write the test file using the file-system tool.
3. **Observe** — run the tests via `subprocess`; capture stdout + exit code.
4. **Adapt** — on `FAILED`, regenerate assertions or fix imports; retry up to N times.
5. **Outcome** — `test_app.py` exists and `unittest` exits `OK`.

This is exactly the agent you implement in [Lab 1](../labs/Lab_1_Introduction_to_Agentic_AI_for_Software_Development.md).

---

## 1.2 Why Agentic AI for Software Engineering?

Software engineering is *the* domain where agentic AI pays off, because it is full of work that is **multi-step, tool-heavy, verifiable, and repetitive**:

- **Verifiable outcomes** — tests pass/fail, builds compile, linters return 0 / non-0. The agent gets a hard signal at every step.
- **Rich tool surface** — shells, language servers, test runners, package managers, CI, Git, code search.
- **Composable tasks** — read → reason → edit → run → review → commit. Perfect for a loop.
- **Toil to automate** — boilerplate tests, dependency bumps, doc updates, log triage, PR responses.

### What you can do with an agent that you cannot do with chat alone

| Capability | Chat assistant | Agentic system |
|---|---|---|
| Write a unit test from a prompt | ✅ produces text | ✅ writes the file |
| Run the test and read the result | ❌ | ✅ via shell tool |
| Fix the test if it fails | ❌ (you iterate) | ✅ adapts and retries |
| Open a PR with the change | ❌ | ✅ via Git/GitHub tool |
| Remember earlier decisions across steps | ❌ | ✅ via memory |
| Refuse to touch protected files | ❌ | ✅ via guardrails |

### Example — Cross-repo dependency agent

> *Goal: "Bump `requests` to `>=2.32` across all microservices and open PRs."*
>
> 1. Discover repos via the Git tool.
> 2. For each repo: open, edit `requirements.txt`, run tests.
> 3. If tests pass → branch, commit, push, open PR with auto-generated changelog.
> 4. If tests fail → log, skip, add a `needs-human` label.

The agent is doing engineering work end-to-end, with verifiable artifacts (PR URLs, test logs).

---

## 1.3 Key Concepts and Terminology

| Term | Definition (in a software-dev context) |
|---|---|
| **Agent** | A loop-driven program that pursues a goal by invoking an LLM + tools and reacting to results. |
| **Goal** | A precise, testable outcome (e.g., "all tests in `backend_app/` pass"). |
| **Agentic loop** | The iterative cycle: **plan → act → observe → adapt**. |
| **Plan** | An ordered list of intended steps the agent will execute. |
| **Act** | A single tool invocation (file write, `subprocess.run`, API call). |
| **Observe** | Reading the *real* result of an action (stdout, exit code, diff). |
| **Adapt** | Revising the plan or the artifact based on an observation. |
| **ReAct** | A common pattern that interleaves reasoning ("Thought:") with actions ("Action:") and observations. |
| **Tool use** | Calling external developer tools (shell, test runner, Git, IDE, MCP server). |
| **Memory** | Persisted context: prior steps, file summaries, decisions, repo facts. |
| **Guardrails** | Validations and policies that constrain what the agent may do or output. |
| **Multi-agent workflow** | Multiple specialized agents (planner, coder, reviewer) coordinating on one goal. |
| **RAG** | Retrieval-Augmented Generation — grounding the agent in your codebase via search/embeddings. |

---

## 1.4 From Module to Lab — Your First Coding Agent

In [Lab 1](../labs/Lab_1_Introduction_to_Agentic_AI_for_Software_Development.md) you implement every concept from §1.1 in ~80 lines of Python. Use this map as you work through it:

| Module 1 concept | Lab 1 implementation |
|---|---|
| **Goal** | The string passed to `agentic_loop("Add a unit test for add() and subtract()...")`. |
| **Plan** | The `plan()` function returning a list of steps. |
| **Act** | The `act()` function that writes `test_app.py` and runs `python -m unittest`. |
| **Observe** | Parsing `subprocess.run(...).stdout` for `OK` / `FAILED`. |
| **Adapt** | The `adapt()` function and the `max_retries` guard. |
| **Tool use** | File I/O + `subprocess` (a real shell tool — expanded in Module 3). |
| **Memory** | (Stubbed in Lab 1; built out in Module 4.) |
| **Guardrails** | `max_retries` is the simplest guardrail; richer policies arrive in Module 4. |

---

## 🎯 Module 1 — Takeaways

1. **An agent is a loop, not a model.** Plan → Act → Observe → Adapt.
2. **Software dev is the killer use case.** Verifiable outcomes + rich tools = ideal agent territory.
3. **Tools, memory, and guardrails are first-class.** They separate a chat reply from a closed-loop engineering system.
4. **Goals must be testable.** "Tests pass" is a goal; "improve quality" is not.
5. **Start small, then add depth.** Lab 1 builds the loop; later modules add prompts, tools, memory, guardrails, multi-agent coordination, RAG, and production concerns.

> ➡️ **Next:**
> - 🧪 Do [Lab 1 — Build the agentic loop](../labs/Lab_1_Introduction_to_Agentic_AI_for_Software_Development.md)
> - 📘 Then read [Module 2 — Prompt Engineering for Software Agents](Module_2_Prompt_Engineering_for_Software_Agents.md)
