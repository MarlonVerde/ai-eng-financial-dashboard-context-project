# Rule Validation Matrix (Phase 3)

## Validation objective

Verify each rule can guide real tasks in this repository, and refine wording where ambiguity exists.

## Rule-by-rule validation

### 01-context-before-change.md

- Real task used for validation: preparing phase docs without touching app code.
- Applicability check:
  - AGENTS.md reviewed before edits.
  - Existing .agents/rules reviewed before creating new guidance.
  - memory-bank reviewed for project context.
- Result: Applicable without changes.

### 02-api-contract-first.md

- Real task used for validation: reviewing backend analytical endpoints and frontend consumption flow.
- Ambiguity detected before refinement:
  - Did not force a minimum test/action set when adding a new endpoint.
- Refinement applied:
  - Added explicit new-endpoint checklist (response_model, backend test, frontend type/adapter update).
- Result: Now actionable for endpoint extensions.

### 03-test-gate.md

- Real task used for validation: execution of backend and frontend tests during repository audit.
- Ambiguity detected before refinement:
  - Cross-layer changes did not explicitly require running both suites.
- Refinement applied:
  - Added mandatory dual-suite run for cross-layer changes.
- Result: Better aligned with this full-stack workflow.

### 04-security-and-config.md

- Real task used for validation: auditing backend CORS configuration and frontend API base strategy.
- Ambiguity detected before refinement:
  - Rule did not explicitly ban wildcard origins with credentials in non-local contexts.
- Refinement applied:
  - Added explicit prohibition for allow_credentials plus wildcard origins in shared/production-like environments.
- Result: Clear security guardrail anchored to current backend config risks.

## Overall phase verdict

- Each rule has a concrete use case in this repository.
- Ambiguous rules were refined with operational checks tied to real backend/frontend tasks.
- Rule set is now more enforceable during PR review and AI-agent-driven changes.