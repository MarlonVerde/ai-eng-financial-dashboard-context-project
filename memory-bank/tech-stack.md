# Tech Stack

## Backend

- Python
- FastAPI
- Pydantic
- Uvicorn
- Pytest + httpx test client

## Frontend

- React
- TypeScript
- Vite
- Vitest
- Recharts
- Tailwind CSS (via project dependencies)

## Dev and runtime

- Docker Compose for local multi-service startup
- Node/NPM for frontend scripts
- Pip for backend dependencies

## Important runtime conventions

- Frontend expects /api proxy in local Vite dev mode.
- Optional frontend override through VITE_API_BASE_URL.
- Backend serves deterministic mock dataset using seed=42 in endpoints.