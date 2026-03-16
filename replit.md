# Ragfolio

A RAG-powered portfolio app. Ask questions about a developer's resume and get AI-generated answers via Gemini.

## Architecture

- **frontend/** — React + Vite + Tailwind CSS, dev server on port 5000. All API calls go to `/api/*` (proxied to backend at port 8000).
- **backend/** — FastAPI (Python, uv), port 8000. Endpoints: `GET /health`, `POST /ask`. Uses chromadb + fastembed for RAG.
- **rag/** — uv package with ChromaDB vector store (`rag/chroma_db/`) and embedding utilities.

## Key Files

- `frontend/vite.config.ts` — Vite config: host=0.0.0.0, port=5000, allowedHosts=true, proxy /api → localhost:8000
- `backend/main.py` — FastAPI app, CORS enabled, runs on localhost:8000
- `backend/rag_query.py` — RAG pipeline: embed question → ChromaDB lookup → Gemini API call
- `rag/chroma_db/` — Persistent ChromaDB vector store (pre-built from resume.txt)

## Workflows

- **Start application** — `cd frontend && npm run dev` (port 5000, webview)
- **Backend** — `cd backend && uv run python main.py` (port 8000, console)

## Environment Variables

- `GEMINI_API_KEY` — Required for the `/ask` endpoint to call the Gemini API

## Running Locally

```bash
# Backend
cd backend && uv run python main.py

# Frontend
cd frontend && npm run dev
```

## Deployment

Configured as a VM deployment. Build frontend, then run backend serving on port 5000.
