# Ticketing

[![CI](https://github.com/daniel-machado/ticketing/actions/workflows/ci.yml/badge.svg)](https://github.com/daniel-machado/ticketing/actions/workflows/ci.yml)

Backend for a ticket sales platform. Event organizers create events, buyers reserve and pay for tickets, and staff check tickets in at the door.

Built with NestJS, TypeScript (strict), PostgreSQL and Prisma.

## Prerequisites

- Node.js >= 24
- npm
- Docker (with the Docker daemon running)

## Running locally

1. Install dependencies:
   ```bash
   npm install
   ```
2. Copy the example environment file and adjust values if needed:
   ```bash
   cp .env.example .env
   ```
3. Start PostgreSQL:
   ```bash
   npm run db:up
   ```
4. Apply database migrations:
   ```bash
   npm run db:migrate
   ```
5. Start the API in watch mode:
   ```bash
   npm run start:dev
   ```
6. Check it's running:
   ```bash
   curl localhost:3000/health
   # {"status":"ok"}
   ```

## Scripts

| Command | Description |
|---|---|
| `npm run start:dev` | Run the API in watch mode |
| `npm run build` | Compile TypeScript to `dist/` |
| `npm run db:up` | Start the PostgreSQL container |
| `npm run db:down` | Stop the PostgreSQL container |
| `npm run db:migrate` | Run Prisma migrations |
| `npm run db:studio` | Open Prisma Studio |
| `npm test` | Run unit tests |
| `npm run test:e2e` | Run e2e tests (requires the database to be up, see `npm run db:up`) |
| `npm run lint` | Lint and auto-fix the codebase |
| `npm run format` | Format the codebase with Prettier |

## Roadmap

1. **Modular monolith** (current phase) — all domains run as modules inside a single NestJS process.
2. **Services with RabbitMQ** — domain modules are extracted into independent services that communicate asynchronously over RabbitMQ.
3. **Kubernetes** — services are deployed and scaled independently on Kubernetes.
