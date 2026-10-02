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

## 3. Non-Functional Requirements & Constraints

- **Hosting & Infrastructure:** Must operate within cloud free-tier limits (Render, Vercel, Supabase) for the MVP demo phase.
- **Architecture:** Modular monolith designed with clean boundaries to allow future microservice extraction.
- **Compute Offloading:** Heavy processing (such as vector embedding generation via sentence transformers) must be handled offline or via lightweight APIs to prevent memory exhaustion on free-tier servers.
