# Steve JNR Furnitures API

Production-oriented NestJS API for the Steve JNR storefront, customer dashboard, and admin console.

## Stack

- NestJS and TypeScript
- PostgreSQL with Prisma ORM
- JWT access and refresh tokens
- class-validator / class-transformer
- Swagger at `/docs`
- Docker Compose for PostgreSQL and the API
- pnpm

## Local setup

```bash
pnpm install
cp .env.example .env
# Start PostgreSQL if it is not already running
pnpm exec prisma migrate deploy
pnpm exec prisma db seed
pnpm run start:dev
```

The API is available at `http://localhost:3000/api/v1`; Swagger is available at `http://localhost:3000/docs`.

The seeded administrator is `admin@stevejnr.com` with the password supplied through `SEED_ADMIN_PASSWORD`. The seed command refuses to run without an explicit password.

## Docker

```bash
docker compose up --build
```

## Useful commands

```bash
pnpm run build
pnpm run test
pnpm run test:e2e
pnpm exec prisma format
pnpm exec prisma validate
pnpm exec prisma migrate dev --name change-name
```

`app.http` contains requests covering public, authentication, customer, support, and admin endpoints. Replace the token variables after logging in.

## Architecture

`src/common` contains shared filters, guards, decorators, pipes, and response infrastructure. `src/database` contains the Prisma service. Feature code is separated under `src/modules` into authentication, catalog, commerce, support, and administration modules. Controllers only validate input and delegate business logic to services; Prisma access stays in services/repositories.

## Environment

Never commit `.env`. Use `.env.example` as the template. Production deployments must provide strong, independent JWT secrets, a managed PostgreSQL connection string, a restricted CORS origin, and payment-provider credentials before enabling live payment adapters.
# steve-jr.
