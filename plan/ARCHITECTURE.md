# System Architecture: Truck GeoMapper & Compliance Copilot

## 1. Architectural Pattern & Philosophy

- **Modular Monolith:** FastAPI backend structured into clean domain modules for future microservice extraction.
- **Fail-Hard Error Handling:** The system fails explicitly and immediately on critical errors (e.g., API failures, invalid payloads, database timeouts), returning structured, descriptive error messages to the client rather than hiding failures.
- **Progressive AI Optimization:** The retrieval stack is designed to evolve from a simple semantic search pattern to a gated, reranked, and optionally hybrid search pipeline without changing the core domain model.

## 2. Request Lifecycle & Data Flow

1. **User Action:** User inputs truck specifications and natural language haul description, then submits.
2. **Cache Check:** Backend checks the response cache for a matching query fingerprint.
   - *If cached:* Instantly bypasses external calls and returns cached payload.
   - *If cache miss:* Proceeds to full processing.
3. **Intent & Risk Gate:** A lightweight classification layer determines whether the request needs full LLM synthesis, a retrieval-only response, or a direct safe-path answer.
   - This reduces unnecessary Groq API usage for trivial or cached requests.
4. **Retrieval & Ranking:**
   - Queries Supabase (`pgvector`) for relevant state DOT regulations and metadata filters.
   - Performs either vector-only, lexical, or hybrid retrieval depending on the query type.
   - Applies a reranking model to reorder the retrieved document chunks by relevance before synthesis.
5. **Routing & Constraint Validation:**
   - Fetches base path geometry from an external routing API.
   - Cross-references route data against truck constraints and policy-relevant RAG chunks.
6. **Response Assembly:**
   - Compose a structured route summary, compliance alerts, and briefing text.
   - Cache the result for future repeats and analytics tracking.
7. **Frontend Rendering:** React client updates state, renders the interactive Leaflet map, and displays route compliance alerts, retrieval summaries, and dashboard metrics.

## 3. Retrieval & Reranking Layer

- **Primary Retrieval:** Semantic similarity over `pgvector` document chunks with metadata filters (state, route type, hazmat, vehicle class, etc.).
- **Optional Hybrid Search:** Combine vector retrieval with keyword / lexical search for edge cases where wording is highly specific or legal language is exact.
- **Re-ranking:** After initial retrieval, pass the top candidate chunks through a reranker to improve ordering and reduce context noise sent to the LLM.
- **LLM Gate:** Only call Groq for final synthesis when the query exceeds a threshold of relevance, novelty, or risk. Lower-risk requests can be answered by filtered retrieval results or a stored template.

## 4. Analytics & Observability

- **Usage Metrics:** Track request volume, latency, cache hit rate, retrieval quality, and compliance alert frequency.
- **Charts & Dashboard:** Recharts or similar charting tools can be used to display route statistics, alert distributions, and system-level health metrics.
- **Operational Safety:** Monitor LLM usage cost and retrieval quality so the system stays within free-tier or low-cost constraints.
