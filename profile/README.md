# Aqtilink

## What this app does
- Social activity feed with join/create flows; three Spring Boot services (user, activity, notification) plus a React/Vite frontend.
- Postgres for data, RabbitMQ for async notifications, Clerk for auth/JWTs.


## Run locally (docker-compose)
1) Prereqs: Docker + Docker Compose.
2) Clone all microservices to a directory
3) Env needs JWK_SET_URI=<"your clerk frontend api url">
             SERVICE_API_KEY=<"your clerk secret key">
4) Start: docker compose up --build
5) Apps:
   - Frontend: http://localhost:5173
   - User svc: http://localhost:8080
   - Activity svc: http://localhost:8081
   - Notification svc: http://localhost:8082
6) Stop: docker compose down

## Run locally (no Docker)
- Backend: install JDK 17, Maven; run mvn spring-boot:run in each service.
- Frontend: Node 18+; npm install && npm run dev.
- Infra: Postgres + RabbitMQ locally (see docker-compose.yml for ports/env).

## Troubleshooting
- Ports already in use: stop conflicting services or change port mappings.
- DB migrations: ensure init SQL ran; check Postgres logs.
- Auth: set Clerk keys and JWKS URL in .env.