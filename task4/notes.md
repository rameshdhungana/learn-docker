# Task 4 — Notes: Name and remove

Summary of what we learned while completing Task 4.

---

## What is `--name` for?

**`--name`** gives the **container** (the running instance) a custom name, not the image.

Example: `docker run --name my-nginx nginx`  
- **Image:** `nginx`  
- **Container name:** `my-nginx`

You can then use that name in other commands: `docker stop my-nginx`, `docker rm my-nginx`, `docker logs my-nginx`, etc.

---

## Why does one image have multiple container IDs?

**Each `docker run` creates a new container.**

- **Image** = one template (e.g. `hello-world`).
- **Container** = one instance. Every time you run `docker run hello-world`, the daemon creates a **new** container with a new ID and name.

So one image can have many containers (one per run). That’s why you see many rows with the same IMAGE but different CONTAINER ID and NAMES in `docker ps -a`.

---

## Random names when you don’t use `--name`

If you don’t use **`--name`**, Docker assigns a **random name** (e.g. `heuristic_sinoussi`, `jolly_shtern`). The daemon picks from built-in word lists; the real unique identifier is the **container ID** (the hex string).

**“Already used”** = on **this machine** only. The daemon checks that no existing container on that host has that name.

---

## How many unique names can Docker generate?

From Docker’s source (Moby `names-generator.go`):

- **Adjectives:** 58  
- **Names (scientists/hackers):** 76  

**Without numeric suffix:** 58 × 76 = 4,408 combinations, minus one (`boring_wozniak` is excluded in code) → **4,407** unique names.

**With suffix (0–9):** 4,407 × 10 = **44,070** possible names.

So the **maximum number of auto-generated unique names** is **44,070**. After that, new containers would get name conflicts and creation can fail (after retries).

---

## What if you run hello-world 45,000 times?

If you run `docker run hello-world` 45,000 times and never remove containers:

- **Runs 1–44,070:** Containers get unique names (some with a digit suffix).
- **Run 44,071 onward:** Name space is exhausted. Container creation can **fail** with a “name already in use” (or similar) error.

You’d also hit **resource limits** (disk under `/var/lib/docker`, memory, process limits) before 45,000, so in practice you’d see name conflicts and/or “no space” / resource errors.
