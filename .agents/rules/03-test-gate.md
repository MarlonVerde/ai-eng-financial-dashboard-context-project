# Rule: Test Gate Per Layer

## Why

This project already includes backend pytest and frontend vitest coverage for key financial calculations and API behavior.
Any meaningful change must pass the layer-specific test gate.

## Required behavior

1. For backend changes, run from backend directory:
   - pytest -q
2. For frontend changes, run from frontend directory:
   - npm test
3. For cross-layer changes (API contract + UI consumption), run both suites.
4. Do not merge rule or code changes that introduce failing tests.
5. If tests are skipped, document exactly why and what remains unverified.

## Good practice observed

- Backend tests cover health, filters, summary, comparison, alerts, and business-type endpoints.
- Frontend tests cover KPI aggregation, monthly sorting across years, and formatting helpers.

## Anti-pattern to avoid

- Claiming a fix without running the relevant test suite.

## Done checklist

- Relevant tests executed.
- Results recorded in change notes or memory-bank status.
- Any warning or known risk documented.
- If both backend and frontend were touched, both suites were executed.