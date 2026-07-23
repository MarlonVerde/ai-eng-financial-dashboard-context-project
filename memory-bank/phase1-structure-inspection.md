# Phase 1 - Repository Structure and Entry Points

## Root structure

- backend/
- frontend/
- docker-compose.yml
- README.md and README.es.md
- AGENTS.md

## Services and startup flow

- docker-compose orchestrates two services:
  - frontend on port 5173
  - backend on port 8000 (plus debug port 5678)
- Backend container starts FastAPI with uvicorn and debugpy.
- Frontend container starts Vite dev server.

## Backend entry points

- App entry point: backend/app/main.py
- API routes and domain logic: backend/app/routes.py
- Health endpoint: /health
- Financial endpoints under /api/metrics*.

## Frontend entry points

- Application mount entry point: frontend/src/main.tsx
- Dashboard composition and data fetch: frontend/src/App.tsx
- Data transforms for KPIs and charts: frontend/src/lib/financial-utils.ts
- Vite proxy for /api requests: frontend/vite.config.ts

## Key conventions observed

- Frontend to backend local integration is expected through Vite proxy to http://backend:8000.
- Optional override via VITE_API_BASE_URL is implemented in App logic.
- Backend currently serves deterministic mock data (seeded) for analytics endpoints.