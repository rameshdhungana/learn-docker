# Task 12 — Web app + database

**Level 5 — Docker Compose (real app)**

## What to do

- Create a `docker-compose.yml` with:
  - A database (e.g. `postgres` or `mysql`) with a volume for data.
  - A web app (e.g. a simple Node/Python/static app) that connects to the DB using the Compose service name as hostname.
- Use `environment` or `.env` for DB password. Run with `docker compose up`, then test the app.

## Commands to learn

- Compose `services`, `volumes`, `environment`
- Connecting app to DB via service name

## Check

- App starts and can read/write to the database.

---

## My questions & notes

_(Add your questions and notes here as you go.)_
