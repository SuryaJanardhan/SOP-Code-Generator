# SOP Code Generator

## End-to-End Flow

```text
                    USER
                      │
          ┌───────────┴───────────┐
          │                       │
       Git URL                 SOP Doc
          │                       │
          └───────────┬───────────┘
                      ↓
               SUPERVISOR / ROOT
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
   SOP ANALYSIS AGENT       GIT/REPO AGENT
          │                       │
   Understand bug +          Sandbox clone
   resolution steps          Repo analysis
          │                   Knowledge Graph
          │                   README summary
          └───────────┬───────────┘
                      ↓
                 ROOT AGENT
                      │
              Understands combined
              SOP + repo context
                      ↓
             Dynamic task planning
                      ↓
          ┌───────────┬───────────┐
          ↓           ↓           ↓
       READ        WRITE        CMD
       AGENT       AGENT       AGENT
          │           │           │
          └───────────┴───────────┘
                      ↓
                CODEBASE CHANGE
                      ↓
              Alternate code snippet
```

---

# Project Structure

```text
sop-code-generator/

├── agents/
│   ├── incident_agent.py
│   ├── retrieval_agent.py
│   ├── rootcause_agent.py
│   ├── patch_agent.py
│   ├── testing_agent.py
│   └── evaluator_agent.py
│
├── rag/
│   ├── embeddings.py
│   ├── vectorstore.py
│   └── retriever.py
│
├── data/
│   ├── sops/
│   ├── codebase/
│   └── incidents/
│
├── tests/
│
├── app.py
├── requirements.txt
└── README.md
```

---

# Tech Stack

- LangGraph
- Qdrant
- Sentence Transformers
- Qwen / Llama
- DeepEval
- RAGAS
- Python
- FastAPI

---

# Workflow

1. User reports an incident.
2. LangGraph orchestrates all agents.
3. Retrieval agent fetches relevant SOPs and code.
4. Vector database searches similar incidents.
5. Root-cause agent analyzes the issue.
6. Patch agent generates a fix.
7. Testing agent executes tests.
8. Evaluator checks quality using DeepEval and RAGAS.
9. Human reviews the result.

---

# Future Improvements

- CI/CD integration
- Slack notifications
- Automated rollback
- Kubernetes deployment
- Monitoring dashboard
- Multi-model routing