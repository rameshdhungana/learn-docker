# Task 3 — Notes: List and inspect

Summary of what we learned while completing Task 3.

---

## What does `ps` stand for?

**Process status.** Same idea as the Unix `ps` command. `docker ps` lists running **containers** (your container processes).

---

## What does `-a` mean?

**All.**

- **`docker ps`** — lists only **running** containers.
- **`docker ps -a`** — lists **all** containers (running and stopped/exited).

---

## Where are Docker images stored?

On your machine, Docker stores images (and containers, volumes) in a **local storage area** managed by the daemon.

**Typical location (Linux):** **`/var/lib/docker/`**

You can list it with:
```bash
sudo ls /var/lib/docker/
```

**What the directories are for:**

| Directory      | Purpose |
|----------------|--------|
| **buildkit**   | Build cache and data for image builds (`docker build`). |
| **containers** | Per-container writable layers and metadata. |
| **engine-id**  | Unique ID for this Docker engine. |
| **network**    | Network configs (bridge, custom networks). |
| **plugins**    | Docker plugins. |
| **rootfs**     | Layer/root filesystem data for containers. |
| **runtimes**   | Runtime data (e.g. runc/containerd). |
| **swarm**      | Docker Swarm state (if used). |
| **tmp**        | Temporary files. |
| **volumes**    | Data for named volumes. |

Image layers may live under **buildkit** and/or **containerd** (e.g. `/var/lib/containerd`), not always in a single `image` folder. Use **`docker images`** to see your images; the daemon uses these dirs to store them. Don’t edit these dirs by hand — let Docker manage them.
