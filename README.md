# 🤖 RAG Q&A LLM Bot — Production-Ready Retrieval-Augmented Generation System

A fully modular, production-grade **Retrieval-Augmented Generation (RAG)** microservice built with **FastAPI**, **FAISS**, **deterministic embeddings**, and a **mock LLM generator** (GitHub-safe but fully pluggable with real models like FLAN‑T5).

This repo includes:
- 📥 Document ingestion
- 🔍 Embeddings + FAISS vector search
- 📚 Top‑K retrieval
- 🧠 Generation pipeline (mock LLM for reproducibility)
- ⚡ FastAPI endpoints (`/ingest`, `/query`, `/debug/...`)
- 📊 Monitoring: Prometheus + Grafana dashboard
- 🐳 Complete Docker support
- 🔁 CI/CD pipelines for GitHub & GitLab
- 🧪 Automated Unit Tests
- 📁 Example docs, queries, REST examples

---
## 🚀 Features
- Deterministic mock embeddings (32‑dim SHA‑based vectors)
- Lightweight FAISS vectorstore
- RAG pipeline: retrieval → synthesis → structured answer
- Debug endpoints for inspecting retrieval & generation stages
- Production-ready architecture with monitoring & Docker

---
## 📁 Project Structure
```
src/
  ├── api.py
  ├── config.py
  ├── ingest_core.py
  ├── embeddings.py
  ├── vectorstore.py
  ├── retriever.py
  ├── generator.py
examples/
data/docs/
tests/
Dockerfile
docker-compose.yml
.github/workflows/ci.yml
```

---
## 📥 Ingest Documents
Documents go inside:
```
data/docs/
```
Run ingestion:
```
POST /ingest
```
This builds `vectorstore/index.faiss` + metadata.

---
## 🔄 Full Query Pipeline
```
POST /query
{
  "question": "What is RAG?"
}
```
Pipeline:
1. Embed question
2. Retrieve top‑3 documents via FAISS
3. Synthesize answer using mock generator
4. Return structured output

Sample response:
```
{
  "query": "What is RAG?",
  "answer": "Answer: a94f3...",
  "sources": [0,1,2]
}
```

---
## 🧠 Debug Endpoints
### 🔍 Examine Retrieval
```
GET /debug/retrieve?q=vector
```
### 🔧 Examine Generator
```
GET /debug/generate?q=rag
```

---
## 🐳 Docker
Build & run:
```
docker compose up --build
```
Service runs at:
```
http://localhost:8002
```

---
## 📊 Monitoring
### Prometheus Metrics
```
http://localhost:8002/metrics
```
### Grafana Dashboard
Import file:
```
grafana/rag_dashboard.json
```

---
## 🧪 Run Tests
```
pytest
```
Tests included for:
- ingestion
- embeddings
- vectorstore build/search
- retriever
- generator
- API health

---
## 🔁 CI/CD
Pipeline includes:
- Install deps → Run tests → Build Docker image → Push to DockerHub
```
.github/workflows/ci.yml
.gitlab-ci.yml
```

---
## 📁 Examples
Examples provided in:
```
examples/
```
Includes queries, batch queries, and REST client file.

---
## 📝 License
MIT
