# Requirements: Truck GeoMapper & Compliance Copilot

## 1. Project Vision & Target Persona

- **Primary User:** An independent commercial truck driver.
- **Scope Progression:**
  - **MVP:** A targeted student project focused on a single driver interface.
  - **Post-MVP / Upgrade:** Expansion into a multi-user, fleet-level management and dispatch control system.

## 2. Core Functional Requirements (MVP Must-Haves)

1. **Truck Specification Input:** The user can input and save vehicle physical dimensions and cargo traits (e.g., height, weight, length, width, hazardous material/propane status).
2. **Natural Language Haul Description:** The user can enter a travel request in plain English (e.g., "Hauling a 14ft tall trailer with propane from Seattle to Portland").
3. **Constraint-Based GPS & Routing:** The system calculates a route using an external routing service, cross-referencing path nodes against physical limits and vector-embedded state DOT regulations.
4. **Active Alerts & Hazard Warnings:** The system highlights route vulnerabilities (e.g., low bridge clearances, weight restrictions, hazmat bans) along the path.
5. **Interactive Map & Rerouting Feedback:** The user views the path on an interactive map alongside compliance breakdowns and RAG-retrieved regulatory guidance.

## 3. Advanced Retrieval & AI Efficiency Requirements (Later Development)

1. **LLM Gate for Cost Control:** The system should decide whether a query requires a full Groq synthesis or can be resolved through cached results, direct routing logic, or a retrieval-only response. The system should store reasoning for such a decision as well.
2. **Re-ranking Layer:** The top retrieved regulatory chunks should be reordered before being sent to the LLM so only the most relevant evidence is considered.
3. **Hybrid Search Support:** The retrieval system should support a combination of semantic search and lexical filtering/keyword matching when legal language or exact document references require it.
4. **Retrieval Quality Monitoring:** The application should measure and log retrieval relevance, latency, and token usage so tuning decisions are grounded in actual behavior.

## 4. Analytics & Reporting Requirements (Later Development)

1. **Route & Compliance Statistics:** The product should be able to summarize alert counts, route patterns, and legal risk trends across repeated user queries.
2. **Dashboard Visualizations:** Charts and summary cards should allow users or operators to inspect route outcomes, alert types, and system performance over time.
3. **Flexible Scope:** The charting system should remain lightweight and modular because the exact analytics shape may evolve during product discovery.

## 5. Non-Functional Requirements & Constraints

- **Hosting & Infrastructure:** Must operate within cloud free-tier limits (Render, Vercel, Supabase) for the MVP demo phase.
- **Architecture:** Modular monolith designed with clean boundaries to allow future microservice extraction.
- **Compute Offloading:** Heavy processing (such as vector embedding generation via sentence transformers) must be handled offline or via lightweight APIs to prevent memory exhaustion on free-tier servers.
- **Cost-Aware AI Design:** LLM and retrieval costs must be controlled through caching, gating, and selective reranking to prevent runaway API usage.
- **Extensibility:** The retrieval and analytics layers should be designed so additional search techniques or chart types can be added without redesigning the full product.
