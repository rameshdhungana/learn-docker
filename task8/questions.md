# Task 8 — Use a named volume

**Level 3 — Volumes & persistence**

## What to do

- Run a container (e.g. `redis` or a custom one that writes to a file) with `-v my-data:/data`.
- Stop the container, remove it, run a new one with the same volume. Verify data persists.

## Commands to learn

- `docker run -v name:/path`
- `docker volume ls`
- `docker volume inspect`

## Check

- Data is still there after removing and recreating the container.

---

## My questions & notes

_(Add your questions and notes here as you go.)_
