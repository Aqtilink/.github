# Aqtilink

## App overview
Aqtilink is a social activity platform where users can discover, create, and join local activities. Connect with others in your community through a modern, real-time activity feed.

## Tech overview
- Social activity feed with join/create flows; three Spring Boot services (user, activity, notification) plus a React/Vite frontend.
- Postgres for data, RabbitMQ for async notifications, Clerk for auth/JWTs.

## Branching
- All microservices have main and dev branches, for now in development when there are no active users we just use main branch
- When app will be actually in production we will use dev for development and main as production branch.
- Right now whe have set up GitHub actions for automatic compiling and pushing dockerimages on both branches.

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
