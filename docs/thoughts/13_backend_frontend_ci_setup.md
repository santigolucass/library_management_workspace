# Backend and Frontend CI Setup

At this stage, the focus was setting up and hardening CI for both backend and frontend to improve delivery confidence and interview evidence quality.

## What was implemented

- Backend CI pipeline with:
  - OpenAPI HTML validation and artifact upload
  - Security checks (`brakeman` + `bundler-audit`)
  - Lint (`rubocop`)
  - Full RSpec suite with PostgreSQL service
  - Dashboard query performance regression spec
- Backend image publishing workflow to GHCR (`main-latest`, `sha-*`).
- Frontend CI pipeline with:
  - Lint
  - Unit tests
  - Build
  - Cypress E2E running against a live backend container image and CI PostgreSQL.
## Prompt Reference

Prompt used for this milestone: [prompts/13_backend_frontend_ci_setup.md](prompts/13_backend_frontend_ci_setup.md)
