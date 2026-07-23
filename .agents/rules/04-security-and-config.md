# Rule: Security and Config Hygiene

## Why

Current backend CORS policy is intentionally permissive for local demo speed.
Without explicit guardrails, permissive defaults can leak into production-oriented workflows.

## Required behavior

1. Keep permissive CORS only for local/demo mode.
2. For deploy-like environments, replace wildcard origins with explicit allowlist.
3. Keep API origin configurable via VITE_API_BASE_URL (frontend) and avoid hardcoding non-local hosts.
4. Track dependency risk signals (for example npm audit output) in project status notes.
5. Never combine `allow_credentials=True` with wildcard origins in shared or production-like environments.

## Good practice observed

- Frontend uses environment-based API base URL with local fallback.

## Anti-pattern to avoid

- Shipping wildcard CORS + credentials in shared or production environments.

## Done checklist

- CORS intent documented for target environment.
- API base URL strategy documented.
- Dependency vulnerability status noted when dependencies are updated.