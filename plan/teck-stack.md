# Tech Stack: Truck GeoMapper & Compliance Copilot

## 1. Frontend & Client Layer

- **Language & Framework:** TypeScript, React
- **Styling:** Tailwind CSS
- **Mapping & Geospatial UI:** Leaflet.js (via React-Leaflet) for interactive map rendering, path polylines, and dynamic danger-zone map overlays (red-zone markers for restrictions).
- **Data Visualization:** Recharts (for rendering route metrics, elevation profiles, or risk analysis graphs).

## 2. Backend & API Layer

- **Language:** Python (3.11+)
- **Framework:** FastAPI (high-performance asynchronous REST API)
- **Data Validation:** Pydantic v2
- **Server:** Uvicorn

## 3. Database & Vector Storage

- **Primary Database:** Supabase (Cloud-hosted PostgreSQL with `pgvector` extension enabled for regulatory document chunks).

## 4. AI, RAG, & Machine Learning

- **Embedding Generation:** Hugging Face Inference API (via lightweight HTTP calls for both offline seed scripts and live user search queries).
- **LLM / Agentic Reasoning:** Groq API (low-latency pre-trip briefing synthesis).

## 5. External Integration APIs

- **Geospatial Routing:** OpenRouteService / Mapbox Directions API (outsourced path geometry, distance, and duration).

## 6. Infrastructure & Deployment

- **Containerization:** Docker & Docker Compose (local dev)
- **Hosting:** Vercel (frontend), Render (backend), Supabase (database)