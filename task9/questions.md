# Task 9 — Bind mount (local folder)

**Level 3 — Volumes & persistence**

## What to do

- Run a container (e.g. `nginx`) with `-v $(pwd)/html:/usr/share/nginx/html`. Create an `html/` folder and put a file in it. Edit the file on the host and refresh the browser—see live changes.

## Commands to learn

- Bind mount: `-v $(pwd)/local-path:/container-path`

## Check

- Changes on the host show up in the container without rebuilding.

---

## My questions & notes

_(Add your questions and notes here as you go.)_
