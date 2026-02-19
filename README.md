# Learn Docker

A hands-on project to learn Docker through real tasks. Work through the tasks in order—each builds on the previous one.

---

## Prerequisites

- [Docker installed](https://docs.docker.com/get-docker/) on your machine
- A terminal and a text editor

---

## Learning Path: Tasks

### **Level 1 — Basics**

#### Task 1 — Run your first container → [`task1/questions.md`](task1/questions.md)
- Run a container from the official `hello-world` image.
- **Commands to learn:** `docker run`
- **Check:** You see "Hello from Docker!" and an explanation message.

#### Task 2 — Run an interactive container → [`task2/questions.md`](task2/questions.md)
- Run `docker run -it ubuntu` (or `alpine`).
- Inside the container: run `cat /etc/os-release`, then `exit`.
- **Commands to learn:** `docker run -it`, difference between image and container.

#### Task 3 — List and inspect → [`task3/questions.md`](task3/questions.md)
- Run `docker ps` (running containers) and `docker ps -a` (all containers).
- Run `docker images` to list images.
- **Commands to learn:** `docker ps`, `docker ps -a`, `docker images`.

#### Task 4 — Name and remove → [`task4/questions.md`](task4/questions.md)
- Run a container with a custom name: `docker run --name my-nginx nginx` (then stop it with Ctrl+C or `docker stop my-nginx`).
- Remove the container: `docker rm my-nginx`.
- **Commands to learn:** `docker run --name`, `docker stop`, `docker rm`.

---

### **Level 2 — Images & Dockerfile**

#### Task 5 — Build a simple image → [`task5/questions.md`](task5/questions.md)
- In `task5/`, create a `Dockerfile` that uses `FROM alpine` and runs `echo "Hello from my image!"` via `CMD`.
- Build: `docker build -t my-hello .` and run: `docker run my-hello`
- **Check:** Output is "Hello from my image!".

#### Task 6 — Add a small app → [`task6/questions.md`](task6/questions.md)
- In `task6/`, add a minimal static file (e.g. `index.html`) and a `Dockerfile` that uses `nginx:alpine` and copies it into `/usr/share/nginx/html/`.
- Build and run with `-p 8080:80`. Open http://localhost:8080 in your browser.
- **Commands to learn:** `COPY`, port mapping `-p host:container`.

#### Task 7 — Multi-stage build (optional) → [`task7/questions.md`](task7/questions.md)
- In `task7/`, write a Dockerfile that builds a simple Go or Node app in one stage and copies only the binary/files into a minimal final image (e.g. `alpine`). Run the final image.

---

### **Level 3 — Volumes & persistence**

#### Task 8 — Use a named volume → [`task8/questions.md`](task8/questions.md)
- Run a container (e.g. `redis` or a custom one that writes to a file) with `-v my-data:/data`.
- Stop the container, remove it, run a new one with the same volume. Verify data persists.
- **Commands to learn:** `docker run -v name:/path`, `docker volume ls`, `docker volume inspect`.

#### Task 9 — Bind mount (local folder) → [`task9/questions.md`](task9/questions.md)
- In `task9/`, run a container (e.g. `nginx`) with `-v $(pwd)/html:/usr/share/nginx/html`. Edit a file in `html/` on the host and refresh the browser—see live changes.

---

### **Level 4 — Networking**

#### Task 10 — Create a custom network → [`task10/questions.md`](task10/questions.md)
- Run `docker network create my-net`.
- Run two containers on `my-net` (e.g. `nginx` and `alpine`). From the `alpine` container, run `wget -qO- http://<nginx-container-name>` (use the other container’s name as hostname).
- **Commands to learn:** `docker network create`, `docker run --network`, DNS between containers.

#### Task 11 — Compose two services → [`task11/questions.md`](task11/questions.md)
- In `task11/`, create a `docker-compose.yml` with a web service (e.g. nginx) and an app service. Put them on the same network and have one call the other by service name.

---

### **Level 5 — Docker Compose (real app)**

#### Task 12 — Web app + database → [`task12/questions.md`](task12/questions.md)
- In `task12/`, create a `docker-compose.yml` with a database (e.g. `postgres` or `mysql`) with a volume, and a web app that connects using the Compose service name as hostname. Use `environment` or `.env` for the DB password. Run with `docker compose up`, then test the app.

#### Task 13 — Add a reverse proxy (optional) → [`task13/questions.md`](task13/questions.md)
- In `task13/` (or extend task12), add a third service (e.g. `nginx` or `traefik`) in front of your web app so all traffic goes through the proxy (single port 80/443).

---

### **Level 6 — Cleanup & hygiene**

#### Task 14 — Clean up → [`task14/questions.md`](task14/questions.md)
- Remove all stopped containers: `docker container prune`. Remove unused images: `docker image prune -a`. Remove unused volumes: `docker volume prune`.
- **Commands to learn:** `prune` variants, when to use `-f` or `-a`.

#### Task 15 — Inspect and debug → [`task15/questions.md`](task15/questions.md)
- Use `docker inspect <container>` and `docker logs <container>` on one of your containers. Run a one-off command in a running container: `docker exec -it <container> sh`.

---

## Folder layout

Each task has its own folder with a **`questions.md`** file. Use it for the task description and add your own questions and notes as you go.

```
learn-docker/
├── README.md
├── TASKS.md
├── task1/
│   └── questions.md
├── task2/
│   └── questions.md
├── task3/
│   └── questions.md
├── task4/
│   └── questions.md
├── task5/
│   └── questions.md
├── task6/
│   └── questions.md
├── task7/
│   └── questions.md
├── task8/
│   └── questions.md
├── task9/
│   └── questions.md
├── task10/
│   └── questions.md
├── task11/
│   └── questions.md
├── task12/
│   └── questions.md
├── task13/
│   └── questions.md
├── task14/
│   └── questions.md
└── task15/
    └── questions.md
```

## How to use this repo

1. Do **one task at a time**; run the commands yourself.
2. Open the task folder (e.g. `task1/`) and read **`questions.md`** for the steps.
3. Add your **questions and notes** in the same `questions.md` as you go.
4. Check off tasks in `TASKS.md` when you finish them.
5. Experiment: change Dockerfiles, add services, break things and fix them.

When you're ready, start with **Task 1** ([`task1/questions.md`](task1/questions.md)) and run:

```bash
docker run hello-world
```

Good luck—you’ve got this.
