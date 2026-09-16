# Smart Document Processing (RAG)

An event-driven agentic document workflow that reads a **resume**, parses a **job application form**, and uses **RAG (Retrieval-Augmented Generation)** to automatically answer the form's fields — with a human-in-the-loop review step (by text and by voice) before the final output is accepted.

Built while working through DeepLearning.AI's *Event-Driven Agentic Document Workflows* course (built in partnership with LlamaIndex), using [LlamaIndex Workflows](https://docs.llamaindex.ai/) as the underlying event-driven agent framework.

> RAG retrieves the information — the agentic workflow orchestrates the complete task.

---

## How it Works

1. **Ingest** — a resume is parsed, chunked, embedded, and loaded into a vector store; a query engine is built on top of it.
2. **Parse the form** — a job application form is parsed and its blank fields are converted into natural-language questions (e.g. *"Field: Years of Experience"* → *"How many years of experience does the candidate have?"*).
3. **Retrieve + Answer** — each question is run through the RAG query engine against the resume to produce an answer.
4. **Human-in-the-loop review** — a human checks the generated answers and can approve them or give feedback, first as text and then by voice; the workflow loops back and re-answers based on that feedback.
5. **Structured output** — once approved, the collected answers are combined into the final filled-out form.

```
Resume ──► parse / embed ──► vector store ──► query engine
                                                    │
Job Application Form ──► parse fields ──► questions ┘
                                                    │
                                              RAG query
                                                    │
                                            generate answer
                                                    │
                                        human reviews output
                                           ↙            ↘
                                      correct        incorrect
                                         │                │
                                      continue      feedback → re-process
```

This is an **event-driven** workflow, not a fixed pipeline: each step emits an event that triggers the next step, which is what makes branching (correct vs. incorrect) and looping (feedback → re-answer) possible.

---

## Notebooks

| Notebook | What it covers |
|---|---|
| [`Building_workflow (1).ipynb`](./Building_workflow%20(1).ipynb) | Sets up the core LlamaIndex Workflow: defining steps, emitting and listening for events, and wiring the event-driven control flow. |
| [`Adding_RAG.ipynb`](./Adding_RAG.ipynb) | Parses the resume, builds embeddings, loads them into a vector store, and creates a query engine for retrieval. |
| [`Form_parsing.ipynb`](./Form_parsing.ipynb) | Parses the job application form and converts its blank fields into a series of RAG-ready questions. |
| [`Human in Loop.ipynb`](./Human%20in%20Loop.ipynb) | Adds a human-in-the-loop review step — approve an answer or send feedback that triggers a re-answer loop. |
| [`Use voice.ipynb`](./Use%20voice.ipynb) | Extends human feedback from text input to voice input for reviewing and correcting answers. |
| [`agentic_workflows_handwritten_notes.html`](./agentic_workflows_handwritten_notes.html) | Handwritten-style study notes summarizing the course concepts and interview Q&A. |

Run the notebooks in the order above — each one builds on the workflow set up in the previous one.

---

## Key Concepts

| Concept | Meaning |
|---|---|
| **Agentic Workflow** | AI performs multiple steps to complete a task, deciding actions along the way |
| **Event** | A signal that something happened, which can trigger the next step |
| **Workflow Step** | One unit of work: takes input/events in, does something, emits an event out |
| **RAG** | Retrieve relevant document info before generating an answer |
| **Vector Store** | Stores embeddings for semantic search over the resume |
| **Query Engine** | The interface used to search the indexed resume data |
| **Human-in-the-Loop (HITL)** | A person reviews, corrects, or approves the AI's output |
| **Branching** | The workflow follows a different path depending on whether the review is correct or incorrect |
| **Looping** | A step repeats — re-answering — when feedback says the result is wrong or incomplete |

---

## Tech Stack

| Layer | Tech |
|---|---|
| Agent orchestration | [LlamaIndex Workflows](https://docs.llamaindex.ai/) (event-driven) |
| Retrieval | RAG — embeddings + vector store + query engine |
| Interface | Jupyter notebooks |
| Human feedback | Text input, then voice input |

---

## Getting Started

### Prerequisites

- Python 3.10+
- Jupyter Notebook / JupyterLab
- An LLM API key (as configured in the notebooks) for embeddings and generation

### Setup

```bash
git clone https://github.com/Rohanhnk/Smart_document_processing-RAG-.git
cd Smart_document_processing-RAG-

python3 -m venv .venv
source .venv/bin/activate

pip install llama-index jupyter
# plus any additional packages imported at the top of each notebook
```

### Run

```bash
jupyter notebook
```

Open the notebooks in this order:

1. `Building_workflow (1).ipynb`
2. `Adding_RAG.ipynb`
3. `Form_parsing.ipynb`
4. `Human in Loop.ipynb`
5. `Use voice.ipynb`

---

## What to Learn Next

- LangGraph and other graph-based agent orchestration frameworks
- Structured outputs and agent state management
- Agent / RAG evaluation
- Deploying the workflow behind an API (FastAPI + Docker)
- Extending beyond resumes/forms to contracts, invoices, or claims processing

---

## License

MIT
