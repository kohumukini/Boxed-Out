# Boxed Out

## Project Overview

An AI-powered geospatial pre-trip routing planner for commercial truck drivers. It bridges the gaps between consumer maps and strict constraints of commercial trucking.

## Reference Documents

- **Requirements:** Read ./plan/REQUIREMENTS.md before planning a new feature or project chunk evaluation.
- **Tech Stack:** Read ./plan/tech-stack.md for the frameworks and tools in use.
- **Architecture:** Read ./plan/ARCHITECTURE.md for the system diagram and project design.

## Core Build and Test Commands

- **Install Dependencies:** Use `uv sync` / `uv pip install -r ...` for Python work, or `npm install` for the frontend when applicable.
- **Run the App:** Use the backend and frontend commands defined in the project README or service-specific docs.

## 🛠️ Code Style & Development Conventions

- **Type Safety:** Strict TypeScript rules apply. Avoid using `any` under any circumstances.
- **Error Handling:** Fail early, fail hard, and use explicit custom exception classes rather than generic errors.
- **Unsure:** If there is uncertainty or a missing requirement, always ask the user before proceeding.
- **Separation of Content:** Break large endpoint logic into focused helper functions or modules with clear responsibility boundaries.

## Current Focus

- [ ] Step 1: **Foundation & Database Schema**
  - Initialize the FastAPI project and structure the app under domain modules (for example: `api/`, `core/`, `services/`, `models/`).
  - Configure Supabase and create PostgreSQL tables for:
    - vehicles (height, weight, axle, hazmat status, mpg, tank size)
    - routes (origin, destination, geometry, constraints)
    - regulatory_docs and document_chunks with `pgvector` enabled for RAG
  - Set up the frontend shell with React + TypeScript and a lightweight map UI for early integration testing.
- [ ] Step 2: **Regulatory RAG Pipeline**
  - Build a parser for DOT regulatory documents (PDF/text chunking).
  - Integrate the Hugging Face inference API to generate embeddings and store them in Supabase.
  - Build a FastAPI endpoint that accepts user queries, performs vector similarity search, and synthesizes a briefing with Groq.
- [ ] Step 3: **Route Engine & Compliance Validation**
  - Integrate route geometry retrieval from a mapping provider and evaluate it against vehicle constraints.
  - Flag low-clearance, hazmat, weight, and roadway restrictions along the path.
  - Produce structured compliance results for the UI and API responses.
- [ ] Step 4: **Frontend Experience & Map UX**
  - Render route geometry and risk overlays on an interactive Leaflet map.
  - Present user inputs, route summary metrics, and compliance alerts in a clear desktop-friendly interface.
- [ ] Step 5: **AI Efficiency & Retrieval Quality**
  - Add an LLM gate to avoid unnecessary Groq calls when the request is low-risk or cacheable.
  - Implement a document re-ranking layer (for example, a cross-encoder or LLM-assisted reranker) after initial retrieval.
  - Evaluate whether a hybrid search approach (semantic + lexical / metadata filtering) improves result quality.
  - Keep retrieval quality scoring and latency metrics visible for tuning during development.
- [ ] Step 6: **Analytics & Demo Polish**
  - Add charts and summary views for route outcomes, compliance alerts, and user behavior trends.
  - Continue hardening caching, environment configuration, and deployment readiness.
  - Validate the end-to-end flow for realistic pre-trip planning scenarios.
