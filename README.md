
# Advanced Software Development with Agentic AI

A hands-on course that teaches modern software engineering **with agentic AI from day one** — using autonomous coding agents (GitHub Copilot Agent Mode, Copilot Coding Agent, Claude Code) inside **GitHub Codespaces** to plan, write, test, review, and ship real code. **AWS Kiro** is introduced as a comparative spec-driven stack.

> **Course objective.** By the end, the learner will **ship a real feature as a merged pull request using agents end-to-end** — taking a GitHub issue from spec → plan → code → tests → review → merge, driven by autonomous agents and human oversight.

---

## Project Overview

This repository contains an 8-module curriculum designed for **students and new developers** who want to learn software engineering as an agentic-AI-native discipline. You will learn how to:

- Operate **autonomous coding agents** (Copilot Agent Mode, Copilot Coding Agent, Claude Code) beyond simple chat.
- Engineer **prompts, specs, and context** that drive agents reliably.
- Connect agents to real developer tools through **MCP (Model Context Protocol)**.
- Apply **memory, guardrails, and permissions** for safe code generation.
- Orchestrate **multi-agent workflows** (e.g., Claude Code plans → Copilot Coding Agent ships the PR).
- Use **agentic RAG** to ground agents in your codebase.
- Run agents in **CI/CD** (headless Claude Code in GitHub Actions, Copilot Code Review on PRs).
- Compare paradigms with **AWS Kiro** (spec-driven, hooks, steering).

> **Out of scope.** This course is about *using and orchestrating* production agents — not building agent frameworks from scratch (LangGraph/CrewAI). Lab 1 keeps a tiny hand-coded loop only as a concept demo.

---

## The Stack

| Layer | Tool | Role |
|---|---|---|
| Dev environment | **GitHub Codespaces** | Cloud VS Code, devcontainer-ready |
| Primary agent | **GitHub Copilot** (Chat, Agent Mode, Coding Agent, Code Review) | In-IDE + autonomous PR workflow |
| Secondary agent | **Claude Code** (CLI + VS Code extension) | Long-horizon, headless, sub-agents |
| Tool protocol | **MCP** | Shared tool layer for both agents |
| CI/automation | **GitHub Actions** | Headless agents, tests, deploys |
| Comparative stack | **AWS Kiro** | Spec-driven, Hooks, Steering |

Models available in Copilot include GPT-5, Claude Sonnet 4.5/Opus 4.5, and Gemini 2.5. Claude Code uses Anthropic models directly (or via Bedrock/Vertex).

---

## Course Architecture

A progressive 8-module skills path. Each lab ends in a real artifact (commit, PR, or passing CI run).

```
Env ─▶ Prompts/Specs ─▶ MCP Tools ─▶ Memory & Permissions ─▶ Build (Full-Stack) ─▶ Test ─▶ Ship (SDLC) ─▶ Operate
```

### Modules Overview

Eight modules, each teaching one capability you need to build full-stack software with agentic AI.

| # | Module | What you'll learn |
|---|--------|-------------------|
| 1 | [Set Up the Agentic Dev Environment](modules/Module_1_Set_Up_the_Agentic_Dev_Environment.md) | Codespaces + Copilot; install Claude Code; Kiro overview; the agent loop |
| 2 | [Drive Agents with Prompts & Specs](modules/Module_2_Drive_Agents_with_Prompts_and_Specs.md) | Communicate intent to coding agents — plan-first, spec-first, diff-only patterns |
| 3 | [Equip Agents with Tools (MCP)](modules/Module_3_Equip_Agents_with_Tools_MCP.md) | Wire existing MCP servers (file, git, db, browser, cloud) into Copilot **and** Claude Code |
| 4 | [Constrain Agents Safely (Memory & Permissions)](modules/Module_4_Constrain_Agents_Safely.md) | `CLAUDE.md`, `.copilot-instructions.md`, allow/deny tool lists, review discipline |
| 5 | [Build Features with Agents (Full-Stack)](modules/Module_5_Build_Features_with_Agents.md) | Backend + frontend feature development driven by agents |
| 6 | [Test with Agents](modules/Module_6_Test_with_Agents.md) | Unit, integration, e2e, and evals — agent-generated and agent-run |
| 7 | [Ship via the Agentic SDLC](modules/Module_7_Ship_via_the_Agentic_SDLC.md) | Issue → PR → Code Review → Merge with Copilot Coding Agent + headless Claude Code in CI |
| 8 | [Operate Agents in Production](modules/Module_8_Operate_Agents_in_Production.md) | CI scaling, cost caps, observability, policy |

> **Note.** Module file names are kept stable to preserve links; the in-file titles match the names above.

---

## Repository Structure

- [docs/index.md](docs/index.md) — Course index and full clickable Table of Contents
- [docs/course_overview.md](docs/course_overview.md) — Tree view of the course structure
- [docs/glossary.md](docs/glossary.md) — Definitions of key terms used across the course
- [modules/](modules) — The 8 module markdown files (theory)
- [labs/](labs) — Hands-on labs for each module
- [CONTRIBUTING.md](CONTRIBUTING.md) — How to contribute to this repository
- [LICENSE](LICENSE) — Project license

---

## Labs: Hands-On Agentic Software Development

Each lab ends in a **real artifact** — a commit, a pull request, or a passing CI run — produced by an agent inside Codespaces.

| # | Lab | Focus |
|---|-----|-------|
| 1 | [Set Up the Agentic Dev Environment](labs/Lab_1_Set_Up_the_Agentic_Dev_Environment.md) | Open Codespace → Copilot Chat → Copilot Agent Mode → ship your first PR. Optional: install Claude Code and compare. |
| 2 | [Drive Agents with Prompts & Specs](labs/Lab_2_Drive_Agents_with_Prompts_and_Specs.md) | Iterate prompts/specs until the agent ships a passing build |
| 3 | [Equip Agents with Tools (MCP)](labs/Lab_3_Equip_Agents_with_Tools_MCP.md) | Wire MCP servers (GitHub, filesystem, Playwright, db) into Copilot **and** Claude Code |
| 4 | [Constrain Agents Safely](labs/Lab_4_Constrain_Agents_Safely.md) | Configure memory files (`CLAUDE.md`, `.copilot-instructions.md`) and tool allow/deny policies |
| 5 | [Build a Full-Stack Feature with Agents](labs/Lab_5_Build_a_Full_Stack_Feature_with_Agents.md) | Agent-driven backend + frontend feature in one app |
| 6 | [Test with Agents](labs/Lab_6_Test_with_Agents.md) | Agent-authored unit, integration, e2e tests + golden-output evals |
| 7 | [Ship via the Agentic SDLC](labs/Lab_7_Ship_via_the_Agentic_SDLC.md) | Issue → Copilot Coding Agent → PR → Copilot Code Review → merge |
| 8 | [Operate Agents in Production](labs/Lab_8_Operate_Agents_in_Production.md) | Headless `claude -p` in GitHub Actions; cost caps, observability, policy |

See the [labs/](labs) directory for all lab files and instructions.

---

## Agent Stacks Used in This Course

| Stack | Role | When you meet it |
|---|---|---|
| **Codespaces + GitHub Copilot** (Chat, Agent Mode, Coding Agent, Code Review) | Primary working environment — preinstalled, $0 path for students | Lab 1 onward |
| **Claude Code** (Anthropic CLI + VS Code extension, runs inside the same Codespace) | Long-horizon autonomy, sub-agents, headless CI | Optional preview in Lab 1; **mandatory from Module 3** |
| **AWS Kiro** (spec-driven IDE, Hooks, Steering, Bedrock-backed) | Comparative paradigm — concepts/capabilities only in Module 1 | Module 5 |
| **MCP (Model Context Protocol)** | Shared tool layer used by all three stacks | Module 3 onward, every lab |

> All three stacks can use Anthropic Claude models. Copilot and Claude Code can coexist in the same Codespace.

---

## Getting Started

1. **Open this repo in a GitHub Codespace** (Code → Codespaces → Create codespace).
2. Sign in to **GitHub Copilot** (free for verified students; Pro from $10/mo).
3. Start with **[Lab 1](labs/Lab_1_Set_Up_the_Agentic_Dev_Environment.md)** — ship your first agentic PR.
4. *(Optional now, required from Module 3)* Install **Claude Code**:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
   Then add your `ANTHROPIC_API_KEY` as a Codespaces secret.
5. Follow the modules in order alongside the labs; reference [docs/glossary.md](docs/glossary.md) as needed.

> **Cost note.** A student-eligible learner can complete most of the course on **$0** (Codespaces free tier + Copilot Free/Pro for students). Claude Code is optional and adds ~$20–$200/mo (Claude Pro/Max) or pay-as-you-go API.

---

## Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## License

This project is released under the terms of the [MIT License](LICENSE).

© 2026 Dr. Georges Bou Ghantous. All rights reserved.

---

<sub><i><span style="color:#B0B0B0">👤 Author: Dr. Georges Bou Ghantous</span></i></sub>
