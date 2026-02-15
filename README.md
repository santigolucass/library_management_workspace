# Library Management System

Full-stack implementation of the **BLA Ruby on Rails Technical Interview Exercise (V2)**.

* Exercise PDF: [`docs/Ruby on Rails - BLA - Technical Interview Exercise - V2.pdf`](docs/Ruby%20on%20Rails%20-%20BLA%20-%20Technical%20Interview%20Exercise%20-%20V2.pdf)
* Backend (Rails API): [`backend/`](backend/)
* Frontend (React + TypeScript): [`frontend/`](frontend/)

---

# Clone and Submodules (Important)

This repository uses git submodules for backend and frontend.

Clone the workspace repository, then initialize/update submodules:

```bash
git clone git@github.com:santigolucass/library_management_workspace.git
cd library_management_workspace
git submodule update --init --recursive --remote
```

The `--remote` flag updates submodules to the latest commits on their configured remote branches (intended to track each submodule `main` branch).

---

# Quick Review Guide

For an efficient technical review:

1. **Requirement traceability** → See *Requirement Coverage* section.
2. **API contract** → [`backend/docs/openapi-v1.yml`](backend/docs/openapi-v1.yml)
3. **Architecture & domain boundaries** → See *Architecture and Design Choices*.
4. **Tests and CI rigor** → See *CI Pipelines*.
5. **GenAI process transparency** → [`docs/thoughts/`](docs/thoughts/)

---

# Overview

This project implements a role-based library management platform with:

* Authentication (`register`, `login`, `logout`)
* Two roles (`librarian`, `member`) with enforced authorization
* Book catalog CRUD (librarian-only write operations)
* Borrowing lifecycle with domain invariants
* Dashboard views for both roles
* Automated tests and security checks

---

## Informal User Story

As a **librarian**, I manage books and monitor borrowing activity to maintain accurate inventory and detect overdue cases.

As a **member**, I authenticate, discover books, borrow available copies, and track due dates.

---

# Requirement Coverage (PDF → Implementation)

## Backend

| Requirement                      | Implementation                                     |
| -------------------------------- | -------------------------------------------------- |
| Register, login, logout          | [`backend/app/controllers/api/v1/auth/`](backend/app/controllers/api/v1/auth/) + OpenAPI |
| Two roles                        | [`backend/app/models/user.rb`](backend/app/models/user.rb) (`role` enum) |
| Librarian-only book write access | [`backend/app/policies/book_policy.rb`](backend/app/policies/book_policy.rb) |
| Book attributes                  | [`backend/app/models/book.rb`](backend/app/models/book.rb) + OpenAPI schema |
| Search by title/author/genre     | [`GET /books?q=`](backend/docs/openapi-v1.yml) |
| Prevent duplicate active borrow  | [`backend/app/services/borrowings/create_service.rb`](backend/app/services/borrowings/create_service.rb) + model constraints |
| Due date = 2 weeks               | Domain logic in service/model                      |
| Librarian marks return           | [`POST /borrowings/:id/return`](backend/docs/openapi-v1.yml) |
| Librarian dashboard metrics      | [`backend/app/services/dashboards/librarian_summary_query.rb`](backend/app/services/dashboards/librarian_summary_query.rb) |
| Member dashboard                 | [`backend/app/services/dashboards/member_summary_query.rb`](backend/app/services/dashboards/member_summary_query.rb) |
| RESTful API + proper statuses    | OpenAPI + request specs                            |

## Frontend

| Requirement         | Implementation                      |
| ------------------- | ----------------------------------- |
| Backend integration | React app consuming Rails API       |
| User-friendly UI    | Feature-based components            |
| CRUD flows          | Auth, books, borrowings, dashboards |
| Structured code     | Feature-oriented modules            |

---

# Architecture and Design Choices

## Contract-First API

The OpenAPI specification ([`backend/docs/openapi-v1.yml`](backend/docs/openapi-v1.yml)) was defined early and used as the implementation reference.

This ensured:

* Consistent response envelopes
* Proper status codes
* Clear alignment between backend, tests, and frontend

---

## Backend Structure

* Controllers handle HTTP transport concerns
* Services encapsulate business logic
* Policies (Pundit) enforce authorization
* Query objects encapsulate dashboard aggregation
* Domain invariants are enforced in both application logic and database boundaries

The goal was clarity and separation of concerns rather than over-layering.

---

## Frontend Structure

Frontend follows a feature-oriented structure:

* `auth`
* `books`
* `borrowings`
* `dashboards`

Shared API utilities and UI primitives reduce duplication.

---

# Tech Stack

## Backend

* Ruby on Rails (API mode)
* PostgreSQL
* Devise + JWT (denylist revocation)
* Pundit
* RSpec + SimpleCov
* RuboCop, Brakeman, bundler-audit

## Frontend

* React + TypeScript + Vite
* Vitest + Testing Library
* Cypress

---

# Quick Start

From workspace root:

```bash
bin/dev
```

Primary wrappers:

* [`bin/dev`](bin/dev) → backend + frontend + db
* [`bin/rspec`](bin/rspec)
* [`bin/postman`](bin/postman)
* [`bin/cypress`](bin/cypress)
* [`bin/cleanup`](bin/cleanup)

---

# Manual Setup (Alternative)

## Backend

```bash
cd backend
bundle install
cp .env.example .env.development
cp .env.example .env.test
docker compose up -d db
bin/rails db:prepare
RAILS_ENV=test bin/rails db:prepare
bin/rails db:seed
bin/rails server -p 3000
```

## Frontend

```bash
cd frontend
npm install
cp .env.example .env
npm run dev
```

Default API base:

```
VITE_API_BASE_URL=http://localhost:3000/api/v1
```

---

# Verification Commands

## Backend

```bash
bundle exec rspec
bin/rubocop
bin/brakeman --no-pager
bin/bundler-audit
```

## Frontend

```bash
npm run lint
npm run test:run
npm run build
npm run test:e2e:run
```

---

## CI Pipelines

CI is implemented separately for backend and frontend to keep quality gates close to each codebase.

---

### Backend CI ([`backend/.github/workflows/ci.yml`](backend/.github/workflows/ci.yml))

Runs on pull requests and pushes to `main` with these jobs:

* **openapi_docs**

  * Lints and validates the OpenAPI specification
  * Uses [`backend/docs/openapi-v1.html`](backend/docs/openapi-v1.html) as generated docs artifact
  * Uploads the generated HTML documentation as a **downloadable GitHub Actions artifact**
* **scan_ruby**

  * Security gates via `bin/brakeman` and `bin/bundler-audit`
* **lint**

  * Style gate via `bin/rubocop -f github`
* **rspec**

  * Full test suite on PostgreSQL service (`RAILS_ENV=test`)
  * Optional N+1 detection (`N_PLUS_ONE_DETECTION=true`)
* **dashboard_performance**

  * Regression spec focused on dashboard query behavior
  * Guards against unintended aggregation or performance regressions

---

### Test and Coverage Strategy (Backend)

The backend test suite validates both correctness and boundaries:

* Request specs for all endpoints (success and error paths)
* Authorization boundary tests (401 / 403)
* Domain rule enforcement tests (409 conflicts for borrowing rules)
* Validation behavior (422 responses and structured errors)
* Service-level specs for core borrowing and return flows

Test coverage is tracked with SimpleCov

---

### Postman Collections

A Postman collection is included for manual and scripted API validation.

* Collection: [`docs/postman/library-management.full-suite.postman_collection.json`](docs/postman/library-management.full-suite.postman_collection.json)
* Environment: [`docs/postman/library-management.local.postman_environment.json`](docs/postman/library-management.local.postman_environment.json)

It can be:

* Imported into Postman UI for interactive exploration
* Executed via [`bin/postman`](bin/postman) for containerized test execution

This provides an additional consumer-facing validation layer beyond automated test suites.

---

### Backend Image Publishing ([`backend/.github/workflows/publish-image.yml`](backend/.github/workflows/publish-image.yml))

On push to `main`, publishes the backend Docker image to GHCR:

* `main-latest`
* `sha-<commit>`

This image is consumed by frontend CI for integration testing against a live backend container.

---

### Frontend CI ([`frontend/.github/workflows/ci.yml`](frontend/.github/workflows/ci.yml))

Runs on pull requests and pushes to `main` with these jobs:

* **lint**: `npm run lint`
* **unit**: `npm run test:run`
* **build**: `npm run build`
* **cypress**

  * Boots PostgreSQL
  * Pulls backend image (`ghcr.io/santigolucass/library-management:main-latest`)
  * Starts a live Rails API container and waits for readiness
  * Runs Cypress E2E tests against the live backend

Cypress tests execute against a real backend container rather than mocks, validating true integration behavior.

---

# Demo Data

Seeded in [`backend/db/seeds.rb`](backend/db/seeds.rb).

Guaranteed credential:

* Librarian: `librarian@demo.local`
* Password: `123123123`

Member accounts are generated dynamically (same password).

---

# Trade-offs and Future Improvements

* JWT denylist chosen for simplicity over rotating refresh tokens.
* Service-based domain layer favored over full DDD to keep clarity.
* Dashboard queries validated via regression specs but not load-tested.
* OpenAPI HTML currently generated locally/CI; could be hosted statically.
* Frontend focuses on clarity and correctness over full design-system polish.

---

# GenAI Usage and Validation

GenAI was used intentionally and iteratively.

Artifacts:

* Planning and architecture notes: [`docs/thoughts/`](docs/thoughts/)
* Prompt history: [`docs/thoughts/prompts/`](docs/thoughts/prompts/)

Validation strategy:

* Compare AI output against OpenAPI contract
* Add tests for edge cases and failure paths
* Review for idiomatic Rails/React structure
* Enforce quality/security gates via CI

---

# Suggested Review Walkthrough (10–15 Minutes)

1. Requirement traceability table
2. OpenAPI contract
3. Role-based authorization boundaries
4. Borrowing conflict rules
5. Dashboards
6. Tests and CI
7. Trade-offs and next steps
