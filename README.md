# LangGraph Agents on SAP BTP

A structured learning repository for building production-grade AI agents with **LangGraph** and deploying them on **SAP Business Technology Platform (BTP)**. Progresses from core concepts through advanced patterns and Cloud Foundry deployment.

---

## Overview

This repo is a hands-on tutorial series covering:

- Core LangGraph primitives (state, nodes, edges, reducers)
- Agentic patterns (ReAct, multi-agent supervisor, subgraphs, RAG)
- SAP BTP integrations (Gen AI Hub, HANA Cloud, OData, Joule Studio)
- Production deployment (FastAPI, streaming, Cloud Foundry, MCP)

All notebook examples are runnable locally without SAP credentials — SAP-specific integrations are clearly marked and include mocked fallbacks.

---

## Learning Path

Work through the notebooks in order:

| # | Notebook | Topics |
|---|----------|--------|
| 0 | [0_langgraph_fundamentals.ipynb](0_langgraph_fundamentals.ipynb) | Setup, state/nodes/edges, conditional routing, tools, ReAct loop, persistence, human-in-the-loop, SAP BTP intro |
| 1 | [1_langgraph_agents_sap_btp.ipynb](1_langgraph_agents_sap_btp.ipynb) | Multi-agent supervisor, subgraphs, parallel execution (Send API), advanced state, HANA RAG, long-term memory, reflection loops, Langfuse observability |
| 2 | [2_langgraph_deployment_sap_btp.ipynb](2_langgraph_deployment_sap_btp.ipynb) | Testing (pytest), FastAPI serving, SSE streaming, AI Core credentials, SAP workflow tools, Cloud Foundry deployment, MCP tools, Joule Studio |
| — | [databricks_interview_prep.ipynb](databricks_interview_prep.ipynb) | PySpark, Delta Lake, medallion architecture, structured streaming, Unity Catalog *(standalone)* |

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Agent framework | [LangGraph](https://github.com/langchain-ai/langgraph) >= 1.0.9 |
| LLM abstraction | LangChain Core + LangChain OpenAI |
| LLM providers | OpenAI (local) / SAP Gen AI Hub (BTP) |
| Persistence | `langgraph-checkpoint-sqlite` (dev), Postgres (prod) |
| Vector search | SAP HANA Cloud (`langchain-hana`) |
| Observability | Langfuse |
| API serving | FastAPI + Uvicorn/Gunicorn |
| Deployment | SAP Cloud Foundry |
| Package manager | [uv](https://github.com/astral-sh/uv) |
| Runtime | Python >= 3.13 |

---

## Setup

**1. Clone and enter the repo**

```bash
git clone <repo-url>
cd langgraph_agents_sap_btp
```

**2. Create a virtual environment and install dependencies**

```bash
uv venv
source .venv/bin/activate      # macOS/Linux
# .venv\Scripts\activate       # Windows

uv sync
```

**3. Configure environment variables**

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=sk-...

# SAP BTP (optional — only needed for BTP-specific cells)
AICORE_AUTH_URL=...
AICORE_CLIENT_ID=...
AICORE_CLIENT_SECRET=...
AICORE_RESOURCE_GROUP=...
AICORE_BASE_URL=...
```

**4. Start Jupyter and open the first notebook**

```bash
jupyter notebook
```

---

## Repository Structure

```
langgraph_agents_sap_btp/
├── 0_langgraph_fundamentals.ipynb      # Start here
├── 1_langgraph_agents_sap_btp.ipynb    # Intermediate patterns
├── 2_langgraph_deployment_sap_btp.ipynb # Production deployment
├── databricks_interview_prep.ipynb     # Databricks/PySpark prep
├── main.py                             # Minimal entry point
├── pyproject.toml                      # Project metadata & dependencies
├── uv.lock                             # Locked dependency versions
└── .env                                # Local credentials (gitignored)
```

---

## Key Concepts Covered

**LangGraph Fundamentals**
- Typed state with `TypedDict` and custom reducers
- Node functions and direct/conditional edges
- Graph compilation and visualization
- Streaming (token-by-token and node-level)

**Agentic Patterns**
- ReAct (Reason + Act) agent loop
- Multi-agent supervisor with handoff
- Subgraphs for modular composition
- Parallel fan-out with the Send API
- Reflection / self-critique loops

**Memory & Persistence**
- Short-term memory via checkpointing
- Long-term memory across conversation threads
- Human-in-the-loop with interrupt/resume

**SAP BTP Integration**
- LLM calls via SAP Generative AI Hub proxy
- Retrieval-Augmented Generation (RAG) with HANA Cloud vector search
- SAP S/4HANA OData tool integration
- BTP Destinations for credential management
- Joule Studio agent registration

**Production Readiness**
- Unit testing agents with pytest and mock LLMs
- FastAPI REST endpoints with SSE streaming
- Cloud Foundry manifest and deployment steps
- Model Context Protocol (MCP) tool integration
- Langfuse tracing and observability

---

## Requirements

- Python 3.13+
- `uv` package manager ([install](https://github.com/astral-sh/uv#installation))
- OpenAI API key (for local development)
- SAP BTP account with AI Core (for BTP-specific sections only)
