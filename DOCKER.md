# Docker Setup

This workspace now provides a shared base compose file and three task-specific compose files.

## 1) Run app (frontend + backend + postgres)

```bash
docker compose -f docker-compose.base.yml -f docker-compose.app.yml up --build
```

App URLs:
- Frontend: http://localhost:5173
- Backend API: http://localhost:3000/api/v1

Notes:
- Backend runs `bin/rails db:prepare` on startup, so migrations are applied automatically.

## 2) Run Postman collection tests

```bash
docker compose -f docker-compose.base.yml -f docker-compose.postman.yml up --build --abort-on-container-exit --exit-code-from postman
```

## 3) Run Cypress tests (headless)

```bash
docker compose -f docker-compose.base.yml -f docker-compose.cypress.yml up --build --abort-on-container-exit --exit-code-from cypress
```

## Cleanup

```bash
docker compose -f docker-compose.base.yml -f docker-compose.app.yml down -v
docker compose -f docker-compose.base.yml -f docker-compose.postman.yml down -v
docker compose -f docker-compose.base.yml -f docker-compose.cypress.yml down -v
```
