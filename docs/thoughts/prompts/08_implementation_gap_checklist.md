# Prompt - Implementation Gap Checklist

You are a senior Rails API reviewer.

I need you to audit the current implementation against `docs/openapi-v1.yml` and produce a practical gap checklist.

Context:
- Milestones 03 to 07 are implemented (environment, testing setup, domain, authentication, authorization).
- The goal is to identify remaining work needed for full contract and interview requirement compliance.
- Project uses Rails API, RSpec, PostgreSQL, and role-based permissions (`librarian`/`member`).

What I need from you:
1. Compare implemented behavior with OpenAPI contract endpoint by endpoint.
2. Identify missing or incorrect behaviors, status codes, and payload shapes.
3. Organize findings into a milestone-oriented checklist (03-07) with concrete tasks.
4. For each gap, suggest exact files likely requiring updates.
5. Include verification commands/tests for each milestone section.
6. Flag high-risk gaps first (authz, conflict semantics, dashboard integrity, contract drift).

Constraints:
- Do not propose changes to API contract unless absolutely necessary.
- Prefer minimal, explicit, test-driven remediation steps.
- Keep checklist actionable and implementation-ready.

Output format:
- Section 1: Summary of coverage vs gaps
- Section 2: Milestone-based checklist (03-07)
- Section 3: File-level touchpoints
- Section 4: Verification commands
- Section 5: Risks and priority order
