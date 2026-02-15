# Prompt - Backend and Frontend CI Setup

You are a senior DevOps and full-stack CI engineer.

I need to implement robust CI for both backend and frontend in a full-stack library management project.

Context:
- Backend: Rails API (security checks, lint, RSpec, performance regression specs)
- Frontend: React + TypeScript (lint, unit tests, build, Cypress)
- API contract source of truth: OpenAPI

What I need:
1. Propose backend GitHub Actions jobs for security, lint, tests, and OpenAPI docs artifact validation.
2. Propose frontend GitHub Actions jobs for lint, unit, build, and Cypress.
3. Add backend image publishing workflow to GHCR and define tagging strategy (`main-latest`, `sha-*`).
4. Configure frontend Cypress to run against a live backend container image and PostgreSQL service.
5. Include reliability details: health checks, readiness waits, failure logs, permissions.
6. Provide a short README section draft explaining CI flow and why it is a strong quality signal.

Constraints:
- Preserve existing app behavior and routes.
- Keep workflows maintainable and readable.
- Prefer practical reliability over theoretical completeness.

Output format:
- Section 1: Assumptions
- Section 2: Workflow files and job structure
- Section 3: Step-by-step implementation
- Section 4: Verification checklist
- Section 5: Risks and mitigations
- Section 6: Any further questions before implementation
