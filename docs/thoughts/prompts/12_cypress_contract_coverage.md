# Prompt - Cypress Suite for OpenAPI-Aligned UI Actions

You are a senior QA automation engineer.

I need a Cypress test suite that validates all key UI actions mapped to the existing OpenAPI contract for the Library Management System.

Context:
- Frontend: React + TypeScript
- Backend: Rails API
- Contract source: `docs/openapi-v1.yml`
- Roles: `librarian` and `member`

Testing goals:
1. Validate authentication flows and protected-route behavior.
2. Validate books flows (search/list and librarian-only write actions).
3. Validate borrowing and returning lifecycle paths.
4. Validate librarian and member dashboards.
5. Validate key negative paths surfaced by API statuses (401/403/404/409/422 where applicable).

Requirements:
- Organize tests by feature and role.
- Use robust selectors and reduce flaky timing assumptions.
- Include setup notes and run command(s).

Output format:
- Section 1: Assumptions
- Section 2: Spec structure and file plan
- Section 3: Test scenarios by feature
- Section 4: Implementation notes
- Section 5: Run and verification checklist
- Section 6: Risks/flakiness mitigation
