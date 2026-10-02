# System Architecture: Truck GeoMapper & Compliance Copilot

## 1. Architectural Pattern & Philosophy

- **Modular Monolith:** FastAPI backend structured into clean domain modules for future microservice extraction.
- **Fail-Hard Error Handling:** The system fails explicitly and immediately on critical errors (e.g., API failures, invalid payloads, database timeouts), returning structured, descriptive error messages to the client rather than hiding failures.

## 2. Request Lifecycle & Data Flow

1. **User Action:** User inputs truck specifications and natural language haul description, then submits.
2. **Cache Check:** Backend checks the response cache for a matching query fingerprint.
   - *If cached:* Instantly bypasses external calls and returns cached payload.
   - *If cache miss:* Proceeds to full processing.
3. **Orchestration & External Processing:**
   - Queries Supabase (`pgvector`) for relevant state DOT regulations.
   - Fetches base path geometry from external Routing API.
4. **Constraint Validation:** Python logic cross-references route data against truck constraints and RAG rules.
5. **Caching & Response:** Newly generated route data is cached, and a structured JSON payload is returned.
6. **Frontend Rendering:** React client updates state, renders the interactive Leaflet map, and displays route compliance alerts.
