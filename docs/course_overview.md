# Course Overview

> **Agentic AI Software Development Focus**
>
> This course is dedicated to the engineering of agentic AI systems—autonomous, goal-driven software agents that plan, act, and adapt in real-world workflows. All modules, docs, and examples are focused on agentic architectures for software engineering, not general software development or unrelated AI topics.

A tree view of the **Agentic AI Software Development** course structure. Each module is a separate file in [`modules/`](../modules); the full clickable index is in [`docs/index.md`](index.md).

## Course Tree

```text
Agentic AI Software Development
│
├── Module 1: Introduction to Agentic AI for Software Development
│   ├── 1.1 What is Agentic AI?
│   ├── 1.2 Why it matters for software engineering
│   └── 1.3 Key concepts and terminology
│
├── Module 2: Prompt Engineering for Software Agents
│   ├── 2.1 Principles of Effective Prompt Engineering
│   ├── 2.2 Backend-Specific Prompt Patterns
│   └── 2.3 Prompt Testing and Iteration
│
├── Module 3: Connecting Agents to Developer Tools
│   ├── 3.1 Integrating with IDEs, CLIs, and APIs
│   ├── 3.2 Model Context Protocol (MCP) basics
│   └── 3.3 Tool registry and invocation patterns
│
├── Module 4: Stateful and Guardrailed Agents
│   ├── 4.1 Memory, context, and session management
│   ├── 4.2 Implementing guardrails for safe code generation
│   └── 4.3 Logging and observability
│
├── Module 5: Multi-Agent Workflows in Software Projects
│   ├── 5.1 Supervisor/worker agent patterns
│   ├── 5.2 Communication and coordination
│   └── 5.3 Workflow orchestration
│
├── Module 6: Agentic RAG for Codebases
│   ├── 6.1 Setting up vector databases for code
│   ├── 6.2 Retrieval-augmented generation for documentation and code
│   └── 6.3 Governance and citation enforcement
│
├── Module 7: AI-Augmented Software Engineering
│   ├── 7.1 Code reading, patch proposal, and test automation
│   ├── 7.2 Simulating pull requests and code reviews
│   └── 7.3 Best practices for AI-in-the-loop development
│
└── Module 8: Productionizing Agentic Systems
    ├── 8.1 Observability, logging, and policy enforcement
    ├── 8.2 Error handling and scaling
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
│   ├── Lab_1_Introduction_to_Agentic_AI_for_Software_Development.md
│   ├── Lab_2_Prompt_Engineering_for_Software_Agents.md
│   ├── Lab_3_Connecting_Agents_to_Developer_Tools.md
│   ├── Lab_4_Stateful_and_Guardrailed_Agents.md
│   ├── Lab_5_Multi_Agent_Workflows_in_Software_Projects.md
│   ├── Lab_6_Agentic_RAG_for_Codebases.md
│   ├── Lab_7_AI_Augmented_Software_Engineering.md
│   └── Lab_8_Productionizing_Agentic_Systems.md
└── modules/
    ├── Module_1_Introduction_to_Agentic_AI_for_Software_Development.md
    ├── Module_2_Prompt_Engineering_for_Software_Agents.md
    ├── Module_3_Connecting_Agents_to_Developer_Tools.md
    ├── Module_4_Stateful_and_Guardrailed_Agents.md
    ├── Module_5_Multi_Agent_Workflows_in_Software_Projects.md
    ├── Module_6_Agentic_RAG_for_Codebases.md
    ├── Module_7_AI_Augmented_Software_Engineering.md
    └── Module_8_Productionizing_Agentic_Systems.md
