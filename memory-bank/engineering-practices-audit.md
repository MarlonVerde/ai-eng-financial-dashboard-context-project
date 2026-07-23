# Engineering Practices Audit (Phase 2)

## Scope

- Backend: FastAPI routes and app config.
- Frontend: React entrypoint and financial transformation utilities.
- Testing: backend pytest and frontend vitest suites.

## Good practices (5+) grouped by category

### Architecture and separation of concerns

1. Domain transformation logic is centralized in helper functions instead of UI components.
   - Evidence: frontend/src/lib/financial-utils.ts lines 21-67.
2. Dashboard UI composes focused components (header, KPI row, charts) instead of a monolithic page.
   - Evidence: frontend/src/App.tsx lines 2-5 and 57-67.

### API contract and typing

3. Backend uses typed Pydantic response models for each analytical endpoint.
   - Evidence: backend/app/routes.py lines 22-63 and endpoint response_model usage in lines 248, 262, 268, 287, 305, 342, 362, 378.
4. Backend query parameters include explicit typing and constraints (for example limit ge/le).
   - Evidence: backend/app/routes.py lines 289-290.

### Data consistency

5. Returned metric lists are normalized in chronological order before response.
   - Evidence: backend/app/routes.py lines 146-147 and usage lines 259, 375, 391.
6. Mock data generation is deterministic for repeatable behavior in tests and local demos.
   - Evidence: backend/app/routes.py lines 94-104 with seed usage in endpoints lines 255, 264, 277, 295, 311, 350, 370, 386.

### Testing

7. Backend test suite covers health, filters, facets, summary, top categories, comparison and alerts.
   - Evidence: backend/tests/test_routes.py lines 29-189.
8. Frontend utilities have unit tests for KPI math, chronological monthly aggregation and formatting.
   - Evidence: frontend/src/lib/financial-utils.test.ts lines 30-106.

## Risks or bad practices (5+) grouped by category

### Security

1. CORS is globally permissive while credentials are enabled, which is unsafe outside local/demo contexts.
   - Evidence: backend/app/main.py lines 9-12.

### Reliability and data modeling

2. Monetary values use float, which can introduce precision drift in financial domains.
   - Evidence: backend/app/routes.py lines 24, 40-42, 48, 52-55.
3. In-memory random mock generation runs per request, so there is no persistence or historical truth source.
   - Evidence: backend/app/routes.py lines 94-104 and endpoint-level generation calls.

### Frontend resilience

4. Error handling path in App hides status/code detail and does not differentiate network vs contract errors.
   - Evidence: frontend/src/App.tsx lines 35-38.
5. Fetch call has no timeout/abort strategy, which can leave prolonged pending states in degraded networks.
   - Evidence: frontend/src/App.tsx lines 15-20 and lifecycle usage lines 29-43.

### Operability and dependency hygiene

6. Frontend dependency install reports known vulnerabilities that should be tracked and triaged.
   - Evidence: npm install/test run output (5 vulnerabilities reported during dependency installation).

## Proposed mitigation set

- Restrict CORS origins by environment and never pair wildcard origins with credentialed requests outside local demo.
- Define a financial precision policy (Decimal in backend domain model or integer cents transport strategy).
- Introduce a data source abstraction layer so mock generation can be replaced without endpoint rewrites.
- Add abort/timeout strategy and richer error telemetry for frontend data fetching.
- Keep dependency-risk tracking in project status and treat high vulnerabilities as scheduled maintenance work.

## Phase 2 completion statement

This audit identifies at least 5 good practices and 5 risks, grouped by category and grounded with direct code evidence.