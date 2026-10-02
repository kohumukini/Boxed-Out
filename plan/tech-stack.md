# Tech Stack: Truck GeoMapper & Compliance Copilot

## 1. Frontend & Client Layer

- **Language & Framework:** TypeScript, React
- **Styling:** Tailwind CSS
- **Mapping & Geospatial UI:** Leaflet.js (via React-Leaflet) for interactive map rendering, path polylines, and dynamic danger-zone map overlays (red-zone markers for restrictions).
- **Data Visualization:** Recharts (for rendering route metrics, elevation profiles, or risk analysis graphs).
- **Prototype Note:** A lightweight static HTML/CSS/JS prototype may be used for early testing, but the maintained application should use the React frontend described above.

## 2. Backend & API Layer

- **Language:** Python (3.11+)
- **Framework:** FastAPI (high-performance asynchronous REST API)
- **Data Validation:** Pydantic v2
- **Server:** Uvicorn

## 3. Database & Vector Storage

- **Primary Database:** Supabase (Cloud-hosted PostgreSQL with `pgvector` extension enabled for regulatory document chunks).
- **Search & Filtering:** Postgres metadata filtering, with future support for hybrid search combining semantic similarity and lexical matching.

## 4. AI, RAG, & Machine Learning

- **Embedding Generation:** Hugging Face Inference API (via lightweight HTTP calls for both offline seed scripts and live user search queries).
- **LLM / Agentic Reasoning:** Groq API (low-latency pre-trip briefing synthesis).
- **Retrieval Optimization:** LLM gating to avoid unnecessary Groq calls, plus a reranking layer for top-k document refinement.
- **Optional Hybrid Retrieval:** Semantic search with lexical fallback or metadata rank fusion for regulatory queries requiring exact legal phrasing.
- **Optional Reranking Providers:** Cross-encoder models or hosted rerank services can be introduced later if retrieval quality needs improvement.

## 5. External Integration APIs

- **Geospatial Routing:** OpenRouteService / Mapbox Directions API (outsourced path geometry, distance, and duration).
- **Analytics / Visualization:** Recharts for route metrics and alert trends; no external analytics API is required unless a dedicated product analytics tool is introduced later.

## 6. Infrastructure & Deployment

- **Containerization:** Docker & Docker Compose (local dev)
- **Hosting:** Vercel (frontend), Render (backend), Supabase (database)
- **Environment Management:** `.env` files for all external service keys, with strict separation between local development and production credentials.
