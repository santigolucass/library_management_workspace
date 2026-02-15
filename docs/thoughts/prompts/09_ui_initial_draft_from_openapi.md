# Prompt - UI Initial Draft from OpenAPI Contract

You are a senior React + TypeScript frontend engineer.

I need you to build an initial frontend draft for a Library Management System using `docs/openapi-v1.yml` as the strict source of truth.

Context:
- Backend API is already implemented and contract-defined.
- Frontend stack: React + TypeScript.
- Roles: `librarian` and `member`.
- Required capabilities include auth, books, borrowings, and dashboards.

What to implement:
1. Route structure and page scaffolding for:
   - Login/Register
   - Books list/search/details
   - Borrowings list + borrow/return flows
   - Librarian dashboard
   - Member dashboard
2. API client layer mapped to existing OpenAPI operations.
3. Role-aware UI behavior consistent with backend authorization.
4. Basic loading/empty/error/success states.
5. Clean feature-based organization for scalability.

Important rules:
- Do not invent endpoints or fields not present in `openapi-v1.yml`.
- Do not bypass role restrictions in UI behavior.
- Keep implementation focused on functional correctness first.

Output format:
- Section 1: Assumptions
- Section 2: Files to create/modify
- Section 3: Implementation steps
- Section 4: Verification checklist
- Section 5: Risks/trade-offs
- Section 6: Any further questions before implementation
