# AGENTS.md

This file is the single source of truth for any human or AI agent working in this repository.

## Project

Ticketing is the backend for a ticket sales platform: event organizers create events, buyers reserve and pay for tickets, and staff check tickets in at the door. The system is built in three phases: **Phase 1** is a modular monolith (this repo) with one module per domain inside a single NestJS process; **Phase 2** splits those modules into independent services that communicate over RabbitMQ; **Phase 3** moves those services onto Kubernetes for independent scaling and deployment.

## Stack

- NestJS + TypeScript (`strict` mode)
- PostgreSQL via Docker Compose
- Prisma ORM
- Jest (unit and e2e tests)
- ESLint + Prettier

## Commands

| Purpose | Command |
|---|---|
| Start the database | `npm run db:up` |
| Stop the database | `npm run db:down` |
| Run migrations | `npm run db:migrate` |
| Open Prisma Studio | `npm run db:studio` |
| Run the API (watch mode) | `npm run start:dev` |
| Build | `npm run build` |
| Unit tests | `npm test` |
| E2E tests (needs the database up) | `npm run test:e2e` |
| Lint | `npm run lint` |
| Format | `npm run format` |

## Architecture rules

- One module per domain, under `src/modules/<name>`.
- A module never queries another module's tables directly; it calls the other module's exported service.
- Controllers are thin: they validate input and delegate to services. Business logic lives in services.
- DTOs are validated with `class-validator`.

## Domain rules

- Money is stored as integers in minor units (e.g. cents) plus an ISO 4217 currency code. Never use floats for money.
- Timestamps are stored in UTC. Events additionally store an IANA timezone (e.g. `America/Sao_Paulo`) for local-time display.
- Order status changes only through explicit, allowed transitions — never by assigning an arbitrary status.

## Conventions

- Commits follow [Conventional Commits](https://www.conventionalcommits.org/), in English.
- Branch names: `feat/CU-<task-id>-<slug>`.
- PR titles start with `[CU-<task-id>]`.

## Don'ts

- Don't add a new dependency without asking first.
- Don't edit an applied migration — create a new one instead.
- Don't commit secrets or `.env` files.

## Before you say you're done

1. Run lint, unit tests and e2e tests, and make sure they pass.
2. List every file you changed and explain what changed and why.
