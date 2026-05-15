# Module 6 — Agentic RAG for Codebases

> 💡 **Hands-on Labs:** For practical exercises that complement this module, see the [labs/](../labs) directory or start with [Lab 6: Agentic RAG for Codebases](../labs/Lab_6_Agentic_RAG_for_Codebases.md).

> **Module goal.** Learn how to combine retrieval (search) with generation (LLMs) to build agents that can answer questions and generate code using up-to-date, relevant context from codebases and docs.

> **Agentic AI Engineering Focus**
>
> This module is about Retrieval-Augmented Generation (RAG): how agents can search, retrieve, and cite information from large codebases and documentation.

## Table of Contents

- [6.1 Vector Databases for Code and Docs](#61-vector-databases-for-code-and-docs)
- [6.2 RAG Patterns and Pitfalls](#62-rag-patterns-and-pitfalls)
- [6.3 Governance, Citation, and Compliance](#63-governance-citation-and-compliance)

---

## 6.1 Vector Databases for Code and Docs

> **Vector databases enable fast, semantic search over code and documentation.**

**Example: Using FAISS for code search in Python**

```python
import faiss
import numpy as np

# Example: Index and search code snippets
snippets = ["def add(a, b): return a + b", "def multiply(x, y): return x * y"]
embeddings = np.array([[0.1, 0.2], [0.2, 0.3]]).astype('float32')  # Placeholder embeddings
index = faiss.IndexFlatL2(2)
index.add(embeddings)

# Search for similar code
query = np.array([[0.1, 0.2]]).astype('float32')
D, I = index.search(query, k=1)
print("Most similar snippet:", snippets[I[0][0]])
```

---

## 6.2 RAG Patterns and Pitfalls

> **RAG combines retrieval (search) with generation (LLM) for better answers.**

**Pattern:**
1. Retrieve relevant code/docs using vector search
2. Provide retrieved context to the LLM as part of the prompt
3. Generate answer or code with citations

**Example: RAG prompt for code Q&A**

```text
You are a coding assistant. Use the following retrieved code snippets to answer the question. Cite the relevant snippet by index.

Snippets:
[0]: def add(a, b): return a + b
[1]: def multiply(x, y): return x * y

Question: How do I multiply two numbers?
```

**Pitfalls:**
- Irrelevant or low-quality retrieval can mislead the LLM
- Always cite sources and show retrieved context to the user

---

## 6.3 Governance, Citation, and Compliance

> **Governance ensures agents use and cite information responsibly.**

**Best practices:**
- Require citations for all generated answers
- Log all retrievals and generations for audit
- Enforce compliance with data boundaries (e.g., no leaking PII)

**Example: Citation enforcement in Python**

```python
def enforce_citation(answer, snippets):
	cited = any(f"[{i}]" in answer for i in range(len(snippets)))
	if not cited:
		raise ValueError("Answer must cite at least one snippet.")
	return True

# Usage
answer = "You can multiply two numbers using [1]."
snippets = ["def add(a, b): ...", "def multiply(x, y): ..."]
enforce_citation(answer, snippets)
```

---

## 🎯 Module 6 — Takeaways

1. **RAG enables agents to answer questions with up-to-date, relevant context.**
2. **Vector databases make code and doc search fast and scalable.**
3. **Governance and citation are essential for trust and compliance.**

> ➡️ **Next:** [Module 7 — AI-Augmented Software Engineering](Module_7_AI_Augmented_Software_Engineering.md)

