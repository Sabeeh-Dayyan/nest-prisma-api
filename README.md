# Articles API: NestJS + Prisma + PostgreSQL

A REST API for publishing articles, with drafts, Swagger documentation and a seeded PostgreSQL database.

![NestJS](https://img.shields.io/badge/NestJS-E0234E?logo=nestjs&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)

## Endpoints

| Method | Path | Description |
|---|---|---|
| `GET` | `/articles` | Published articles |
| `GET` | `/articles/drafts` | Unpublished drafts |
| `GET` | `/articles/:id` | One article |
| `POST` | `/articles` | Create an article |
| `PATCH` | `/articles/:id` | Update an article |
| `DELETE` | `/articles/:id` | Delete an article |

Interactive docs (Swagger UI) are served at **http://localhost:3000/api**.

An article has `title` (unique), `description` (optional), `body`, `published` (default `false`),
and `createdAt` / `updatedAt` timestamps.

## Run it locally

Requires Node.js and Docker.

```bash
npm install

# 1. Start PostgreSQL
docker compose up -d

# 2. Point Prisma at it
echo 'DATABASE_URL="postgresql://user:1234@localhost:5432/articles?schema=public"' > .env

# 3. Create the tables and add sample articles
npx prisma migrate dev
npx prisma db seed

# 4. Start the API with live reload
npm run start:dev
```

The credentials above are the local-only defaults from `docker-compose.yml`. `.env` is git-ignored.

## Tests

```bash
npm test          # unit tests
npm run test:e2e  # end-to-end tests
```

## Project structure

```
src/
  articles/        controller, service, DTOs and Swagger entity
  prisma/          PrismaService shared across modules
  main.ts          bootstrap + Swagger setup
prisma/
  schema.prisma    Article model
  migrations/      SQL migrations
  seed.ts          sample articles
docker-compose.yml PostgreSQL 13
```
