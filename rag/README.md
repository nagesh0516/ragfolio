# RAG

uv project: chromadb, fastembed, requests. Minimal package for use by the backend (e.g. from `rag_query`).

## Install

```bash
uv sync
```

## Create Embeddings


Package is `rag` (see `rag/rag/__init__.py`). Extend with RAG logic and call from the backend’s `rag_query` module.
