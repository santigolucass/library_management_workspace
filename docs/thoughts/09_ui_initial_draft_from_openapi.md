# UI Initial Draft from OpenAPI Contract

After backend milestone `08_implementation_gap_checklist.md`, the next step was building the initial UI draft using `docs/openapi-v1.yml` as source of truth.

## Goal

Create a first functional frontend draft that mirrors backend capabilities and roles without inventing behavior outside the contract.

## Scope

- Implement core screens and routes for authentication, books, borrowings, and dashboards.
- Use contract-aligned request/response handling for all user actions.
- Keep role-based behavior explicit in UI flow (`librarian` vs `member`).
- Build reusable API and UI foundations for later review/refinement.

## Key Decisions

- Contract-first UI development: every view/action maps to existing endpoints.
- Feature-oriented structure to reduce coupling and support targeted refactors.
- Error states standardized from API payloads (`error` and `errors`) to avoid ad-hoc handling.

## Output

- First end-to-end usable frontend draft integrated with the Rails API.
- Baseline components and route structure ready for design and architecture review.
- Clear mapping between OpenAPI operations and UI interactions.


## Prompt Reference

Prompt used for this milestone: [prompts/09_ui_initial_draft_from_openapi.md](prompts/09_ui_initial_draft_from_openapi.md)
