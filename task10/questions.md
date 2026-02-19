# Task 10 — Create a custom network

**Level 4 — Networking**

## What to do

- Run `docker network create my-net`.
- Run two containers on `my-net` (e.g. `nginx` and `alpine`). From the `alpine` container, run `wget -qO- http://<nginx-container-name>` (use the other container's name as hostname).

## Commands to learn

- `docker network create`
- `docker run --network`
- DNS between containers (name = hostname)

## Check

- One container can reach the other by container name.

---

## My questions & notes

_(Add your questions and notes here as you go.)_
