# Event-Driven Agentic Document Workflows

A short course by **DeepLearning.AI**, built in partnership with **LlamaIndex**.

> RAG retrieves the information — the agentic workflow orchestrates the complete task.

- **Instructor:** Laurie Voss (VP of Developer Relations, LlamaIndex), with contributions from Logan Markewich (LlamaIndex) and Hawraa Salami (DeepLearning.AI)
- **Course link:** https://www.deeplearning.ai/courses/event-driven-agentic-document-workflows
- **Learn platform:** https://learn.deeplearning.ai/courses/event-driven-agentic-document-workflows

---

## 🧠 What This Course Is About

Agentic document workflows are agent-based applications used to automate an **end-to-end document processing task**. While plain RAG just answers questions about your data, an agentic workflow is built on top of RAG to process documents in a more sophisticated, multi-step way:

1. An agent identifies the key information it needs.
2. It retrieves relevant material using RAG.
3. It combines the collected information into a **structured output**.

**Example use cases covered conceptually:**
- Reviewing a contract for regulatory compliance — parse clauses, match against a knowledge base via RAG, generate a compliance summary.
- Enriching invoices with standardized product data — extract item descriptions, match to a product catalog via RAG, append standardized info.

**The hands-on project:** build an agent that reads a **resume** and uses it to fill out a **job application form**, using [LlamaIndex Workflows](https://docs.llamaindex.ai/) — an event-driven architecture for building agents.

---

## 📚 Syllabus

| # | Lesson | Format | Length |
|---|--------|--------|--------|
| 1 | Introduction | Video | 3m |
| 2 | What are Agentic Document Workflows | Video | 5m |
| 3 | Building a Workflow | Video + Code | 18m |
| 4 | Adding RAG | Video + Code | 9m |
| 5 | Form Parsing | Video + Code | 6m |
| 6 | Human in the Loop | Video + Code | 8m |
| 7 | Use your Voice | Video + Code | 6m |
| 8 | Conclusion | Video | 1m |
| 9 | Quiz (Graded) | Quiz | 10m |
| 10 | Appendix – Tips and Help | Code Example | 10m |

---

## 🧩 Key Concepts

| Concept | Simple meaning |
|---|---|
| **Agentic Workflow** | AI performs multiple steps to complete a task, deciding actions along the way |
| **Event** | A signal that something happened, which can trigger the next step |
| **Workflow Step** | One unit of work: takes input/events in, does something, emits an event out |
| **RAG** | Retrieve relevant document info before generating an answer |
| **Vector Store** | Stores embeddings for semantic search |
| **Query Engine** | The interface used to search indexed document data |
| **Human-in-the-Loop (HITL)** | A person reviews, corrects, or approves the AI's output |
| **Structured Output** | Predictable, machine-usable output (not free text) |

**Intermediate ideas:**
- **Branching** — the workflow follows a different path depending on an intermediate result
- **Looping** — a step repeats if the answer is incomplete, wrong, or needs feedback
- **Concurrency** — independent tasks (e.g. multiple form questions) run without waiting on each other
- **Event collection** — a later step waits for multiple events before continuing
- **Async execution** — long-running work doesn't block unrelated steps

---

## 🏗️ Architecture Mental Model

```
SOURCE DOCUMENT
   ↓
parse / index document
   ↓
embeddings + vector store
   ↓
query engine
   ↓
form → parse fields → generate questions
   ↓
RAG query → retrieve info → generate answer
   ↓
human reviews output
   ↙          ↘
correct      incorrect
   ↓             ↓
continue     feedback → re-process
```

A sequential pipeline looks like `A → B → C → D`.
An **event-driven** workflow looks like `A → event → B → event → C → event → D` — each step fires an event, and that event wakes the next step, which is what makes branching, looping, and concurrency possible.

---

## 🛠️ What You'll Build

A form-filling agent, step by step:

1. Set up RAG: parse a resume → load into a vector store → build a query engine.
2. Parse a job application form and convert its blank fields into a series of questions.
3. Send those questions through the RAG pipeline to get answers.
4. Add human-in-the-loop feedback — first as text, then by voice — and iterate on the returned answers.

---

## 💼 Real-World Applications

| Industry | Example |
|---|---|
| HR | Resume → questions → RAG answers → candidate form |
| Finance | Invoice/document processing and enrichment |
| Legal | Extract clauses and validate them against source documents |
| Healthcare | Process intake forms and supporting documents |
| Insurance | Process claims and supporting evidence |
| Enterprise | Internal document/form workflows with human approval |
| Compliance | Check documents against policies or requirements |

---

## 🗺️ How This Builds on RAG

```
RAG foundations
   ↓
Embeddings + Vector Search + Retrieval
   ↓
Tool Calling / Agents / Reasoning
   ↓
Event-Driven Workflows
   ↓
Branching + Loops + Concurrency
   ↓
Human-in-the-Loop + Voice / Multimodal Interaction
   ↓
Production Agentic Application
```

---

## ✅ Prerequisites

- Basic Python
- Familiarity with RAG concepts (embeddings, vector stores, retrieval) is helpful but not required — the course reintroduces them in context.

## 📦 Tech Used

- [LlamaIndex Workflows](https://docs.llamaindex.ai/) (event-driven agent framework)
- A vector store for RAG (as set up in the course notebooks)
- LLM of choice for generation

---

## 🎯 One-Minute Takeaway

> Instead of a simple sequential RAG pipeline, this course teaches an event-driven workflow where events connect steps and enable branching, looping, and concurrent execution. The document-processing flow parses a source document, uses RAG to retrieve relevant information, turns form fields into questions, generates answers, and incorporates human feedback — RAG handles retrieval, while the event-driven agentic workflow orchestrates the full multi-step task.

## 📌 What to Learn Next

- LlamaIndex Workflows (deeper dive)
- LangGraph and graph-based agent orchestration
- Agent state and structured outputs
- Agent and RAG evaluation
- FastAPI + Docker for deployment
- Build a real document-processing project of your own

---

*Notes compiled from the course syllabus and an accompanying study guide, in the style of a course README.*
