# Cypress Suite for Contract-Covered UI Actions

With frontend behavior and architecture stabilized, I requested a Cypress suite covering all user-facing actions derived from the OpenAPI contract.

## Goal

Provide automated confidence for full-stack behavior across the UI, including role-based flows and critical edge cases.

## Scope

- Authentication flows
- Role-aware book actions (member vs librarian)
- Borrowing and returning lifecycle
- Dashboard behaviors for both roles
- Failure-path checks where UI should show contract-driven API errors

## Key Decisions

- Prioritize high-value end-to-end scenarios over brittle low-level UI details.
- Keep tests aligned to contract behavior and visible user outcomes.
- Reuse stable selectors/patterns to reduce flakiness.

## Outcome
- Better confidence that frontend actions remain synchronized with backend contract behavior.

## Verification

- Execute E2E via workspace wrapper: `bin/cypress`.
- Confirm suite covers critical role paths and status-driven UI responses.


## Prompt Reference

Prompt used for this milestone: [prompts/12_cypress_contract_coverage.md](prompts/12_cypress_contract_coverage.md)
