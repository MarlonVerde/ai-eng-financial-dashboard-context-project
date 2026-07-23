# Rule: API Contract First

## Why

Frontend depends on backend API contract from /api/metrics and related endpoints.
Contract drift quickly causes runtime or chart computation errors.

## Required behavior

1. If backend response shape changes, update frontend types first in frontend/src/lib/financial-types.ts.
2. Keep endpoint filters explicit and typed in FastAPI query params.
3. Preserve deterministic demo behavior for tests (seeded mock generation), unless migration plan is included.
4. Add or adjust tests when endpoint behavior is changed.
5. When adding a new analytics endpoint, include:
	- response_model in FastAPI route decorator
	- at least one backend test that validates payload shape and a filter/constraint behavior
	- frontend type or adapter update if the endpoint is consumed by UI

## Good practice observed

- Backend models use Pydantic response models.
- Frontend transformation logic is isolated in financial-utils.ts.

## Anti-pattern to avoid

- Returning untyped or inconsistent payloads that bypass TypeScript and tests.

## Done checklist

- Response model and TS type alignment checked.
- API behavior covered by backend tests.
- Frontend transform/consumption logic validated by tests or manual checks.
- If a new endpoint was added, contract checklist items are completed.