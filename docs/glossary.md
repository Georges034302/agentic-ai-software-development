# Glossary — Advanced Software Development with Agentic AI

**Agentic AI** — Autonomous, goal-driven AI systems that plan, act, observe, and adapt to complete real-world tasks (here: software-engineering tasks).

**Agent loop** — The plan → act → observe → adapt cycle that defines agentic behavior (Module 1 §1.1).

**Agent vs. model** — The *model* is the LLM (e.g., Claude Sonnet 4.5, GPT-5). The *agent* is the harness around it that runs the loop, calls tools, and manages memory.

**Autonomy spectrum** — Autocomplete → chatbot → pair programmer → autonomous agent. Higher autonomy = longer horizons, less human review per step.

---

## Stacks & Platforms

**GitHub Codespaces** — Cloud-hosted VS Code dev environment, configured by `.devcontainer/`. Default working environment for this course.

**GitHub Copilot** — GitHub's family of coding agents available in Codespaces. Includes:
- **Copilot Chat** — conversational Q&A over your code.
- **Copilot Edits** — coordinated multi-file changes.
- **Copilot Agent Mode** — autonomous in-IDE agent (plans, edits, runs terminal/tests).
- **Copilot Coding Agent** — cloud agent assigned to GitHub Issues; opens PRs.
- **Copilot Code Review** — AI reviewer on pull requests.

**Claude Code** — Anthropic's terminal-first coding agent (CLI + VS Code/JetBrains extensions). Optional in Lab 1; **mandatory from Module 3**. Supports headless mode (`claude -p`) for CI use.

**AWS Kiro** — Spec-driven IDE (VS Code fork) with **Specs**, **Hooks**, and **Steering** files; Claude models via **Amazon Bedrock**. Introduced as a comparative paradigm in Module 5.

**Devcontainer** — `devcontainer.json` config that defines the Codespaces image, features, extensions, and post-create commands.

---

## Protocols & Engineering Surfaces

**MCP (Model Context Protocol)** — Open protocol that exposes tools (filesystem, GitHub API, databases, browsers, AWS, etc.) to agents. Used by Copilot, Claude Code, and Kiro alike. Configured via `.vscode/mcp.json` (Codespaces) or `.kiro/settings/mcp.json` (Kiro).

**Tool** — A capability an agent can invoke (read file, run shell, call API). Tools are typically delivered via MCP servers.

**Memory** — Persistent context an agent reads each session: `CLAUDE.md` (Claude Code), `.github/copilot-instructions.md` (Copilot), Kiro **Steering** files.

**Guardrails** — Mechanisms that constrain agent behavior: tool allow/deny lists, permission prompts, sandboxing, max-iteration limits, policy checks in CI.

**Sub-agents** — Agents spawned by a parent agent for parallel or specialized work (native in Claude Code).

**Headless agent** — An agent run non-interactively, typically in CI (`claude -p "..."`, Copilot Coding Agent).

---

## Workflow Concepts

**Multi-agent workflow** — Two or more agents collaborating (e.g., Claude Code plans, Copilot Coding Agent ships the PR).

**Spec-driven development** — Kiro's paradigm: write `requirements.md` → `design.md` → `tasks.md`, then let the agent execute.

**RAG (Retrieval-Augmented Generation)** — Grounding agent answers in retrieved code/docs to reduce hallucination and enforce citations.

**Hooks (Kiro)** — Event-triggered automations (e.g., on file save, on commit) that invoke an agent.

**AI-in-the-loop SDLC** — Software lifecycle where agents handle parts of issue triage, coding, testing, and review, with humans approving merges.

**Observability** — Logging and monitoring agent actions, tool calls, token cost, and outcomes — essential for production (Module 8).
