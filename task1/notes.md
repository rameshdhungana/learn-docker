# Task 1 — Notes: How Docker works

Summary of what we learned while completing Task 1.

---

## How Docker works (the basics)

When you run `docker run hello-world`, this is what happens:

1. **Docker client** — The `docker` command you type. It doesn’t run containers; it sends commands to the daemon.
2. **Docker daemon** — A background service (`dockerd`) on your machine. It pulls images, creates and runs containers, and manages everything.
3. **Image** — A read-only template (files + metadata). You don’t run an image; you run a **container** from it.
4. **Container** — A running (or stopped) instance of an image. The daemon creates it, adds a writable layer, and runs the process.
5. **Registry / Docker Hub** — Where images are stored and downloaded from (like “GitHub for images”). Remote; it does **not** run your containers.

**Flow:** You → client → daemon → (pull image from Hub if needed) → create container → run process → output back to your terminal.

---

## Where does the daemon run?

**On your local machine.** When you install Docker, you install the daemon on that computer. Docker Hub and other registries are only for storing and serving images; they don’t run your containers.

---

## What gets installed (Fedora example)

**Add Docker’s repo:**
```bash
sudo dnf config-manager addrepo --from-repofile https://download.docker.com/linux/fedora/docker-ce.repo
```
This only adds the repository; it doesn’t install anything.

**Install packages:**
```bash
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

| Package | What it is |
|--------|-------------|
| **docker-ce** | Docker Engine — the **daemon** (the “server” that runs containers). |
| **docker-ce-cli** | The **client** — the `docker` command you use in the terminal. |
| **containerd.io** | Low-level **container runtime** — the daemon uses it to create and run containers. |
| **docker-buildx-plugin** | Extra **build** features (e.g. multi-platform builds). |
| **docker-compose-plugin** | **Compose** — run multi-container apps with `docker compose`. |

---

## When to use plain Docker vs Docker Compose

**Plain Docker (`docker run`, single container):**
- One container (e.g. nginx, a script, hello-world).
- Quick experiments, learning, one-off runs.

**Docker Compose (`docker-compose.yml` + `docker compose up`):**
- **Multiple containers** that work together (e.g. web app + database + Redis).
- One file describes the whole stack; one command starts it all.
- Use when services need to talk to each other or you want a reproducible multi-service setup.

**Rule of thumb:** One container → plain Docker. Two or more that need to work together → Compose.
