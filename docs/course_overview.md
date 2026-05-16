# Course Overview

> **Advanced Software Development with Agentic AI**
>
> This course teaches modern software engineering **with agentic AI from day one**. Students use autonomous coding agents — **GitHub Copilot Agent Mode**, **Copilot Coding Agent**, and **Claude Code** — inside **GitHub Codespaces** to plan, write, test, review, and ship real code. **AWS Kiro** is introduced as a comparative spec-driven stack in Module 5.
>
> **Goal:** ship a real feature as a merged pull request using agents end-to-end (issue → spec → plan → code → tests → review → merge).
>
> **Out of scope:** building agent frameworks from scratch (LangGraph/CrewAI). The course is about *using and orchestrating* production agents.

A tree view of the course structure. Each module lives in [`modules/`](../modules); the full clickable index is in [`docs/index.md`](index.md).

## The Stack

| Layer | Tool |
|---|---|
| Dev environment | GitHub Codespaces |
| Primary agent | GitHub Copilot (Chat, Agent Mode, Coding Agent, Code Review) |
| Secondary agent | Claude Code (CLI + VS Code extension) — optional in Lab 1, mandatory from Module 3 |
| Tool protocol | MCP (Model Context Protocol) |
| CI / automation | GitHub Actions |
| Comparative stack | AWS Kiro (Module 5) |

## Course Tree

Eight skill modules, taught for their own sake.

```text
Advanced Software Development with Agentic AI
│
├── Module 1: Set Up the Agentic Dev Environment
│   ├── 1.1 The agent loop (plan → act → observe → adapt)
│   ├── 1.2 The agentic stacks landscape (Codespaces+Copilot, Claude Code, Kiro)
│   ├── 1.3 Core concepts: agent vs model, tools, MCP, memory, guardrails, autonomy
│   └── 1.4 Your environment: Codespaces, Copilot, optional Claude Code
│
├── Module 2: Drive Agents with Prompts & Specs
│   ├── 2.1 Principles of effective prompts and specs
│   ├── 2.2 Patterns for coding agents (plan-first, test-first, diff-only)
│   └── 2.3 Iterating with Copilot and Claude Code
│
├── Module 3: Equip Agents with Tools (MCP)
│   ├── 3.1 MCP basics and the tool ecosystem
│   ├── 3.2 Configuring MCP servers in Codespaces (Copilot + Claude Code)
│   └── 3.3 Invocation patterns and existing servers (file, git, db, browser, cloud)
│   └── ⚙ Claude Code becomes mandatory from this module onward.
│
├── Module 4: Constrain Agents Safely (Memory & Permissions)
│   ├── 4.1 Memory: CLAUDE.md, .copilot-instructions.md, session context
│   ├── 4.2 Permissions: allow/deny tool lists, sandboxing, review discipline
│   └── 4.3 Logging and basic observability
│
├── Module 5: Build Features with Agents (Full-Stack)
│   ├── 5.1 Agent-driven backend (APIs, data)
│   ├── 5.2 Agent-driven frontend (UI, types)
│   └── 5.3 Wiring it together end-to-end in one app
│
├── Module 6: Test with Agents
│   ├── 6.1 Agent-authored unit and integration tests
│   ├── 6.2 End-to-end tests with browser MCP
│   └── 6.3 Evals and golden-output regression checks
│
├── Module 7: Ship via the Agentic SDLC
│   ├── 7.1 Copilot Coding Agent: assigned issues → PRs
│   ├── 7.2 Copilot Code Review on pull requests
│   └── 7.3 Headless Claude Code in GitHub Actions
│
└── Module 8: Operate Agents in Production
    ├── 8.1 Observability, logging, policy enforcement
    ├── 8.2 Cost caps, error handling, scaling
    └── 8.3 Deployment strategies
```

## Repository Layout

```text
agentic-ai-software-development/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── docs/
│   ├── course_overview.md    # This file
│   ├── glossary.md           # Key terms and definitions
│   └── index.md              # Clickable course index / TOC
├── labs/
│   ├── Lab_1_Set_Up_the_Agentic_Dev_Environment.md
│   ├── Lab_2_Drive_Agents_with_Prompts_and_Specs.md
│   ├── Lab_3_Equip_Agents_with_Tools_MCP.md
│   ├── Lab_4_Constrain_Agents_Safely.md
│   ├── Lab_5_Build_a_Full_Stack_Feature_with_Agents.md
│   ├── Lab_6_Test_with_Agents.md
│   ├── Lab_7_Ship_via_the_Agentic_SDLC.md
│   └── Lab_8_Operate_Agents_in_Production.md
└── modules/
    ├── Module_1_Set_Up_the_Agentic_Dev_Environment.md
    ├── Module_2_Drive_Agents_with_Prompts_and_Specs.md
    ├── Module_3_Equip_Agents_with_Tools_MCP.md
    ├── Module_4_Constrain_Agents_Safely.md
    ├── Module_5_Build_Features_with_Agents.md
    ├── Module_6_Test_with_Agents.md
    ├── Module_7_Ship_via_the_Agentic_SDLC.md
    └── Module_8_Operate_Agents_in_Production.md
