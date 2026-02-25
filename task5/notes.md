# Task 5 — Notes: Build a simple image

Summary of what we learned while completing Task 5.

---

## What is Alpine?

**Alpine** = **Alpine Linux** — a very small Linux distribution. The **`alpine`** image on Docker Hub is the official image for it.

- **Small** — base image is only a few MB.
- **Minimal** — few packages by default (musl, BusyBox).
- **Good as a base** when you only need a shell or a tiny app (e.g. `echo "Hello from my image!"`).

Compared to **Ubuntu** images (much larger), Alpine is for the smallest possible base.

---

## What does `CMD` do?

**`CMD`** sets the **default command** (and arguments) that run when a container **starts** from that image.

- **Exec form (preferred):** `CMD ["executable", "arg1", "arg2"]` — array of strings: first = program, rest = arguments. No shell; use **double quotes** in the Dockerfile (single quotes are invalid).
- **Shell form:** `CMD echo "hello"` — runs via `/bin/sh -c`. JSON/exec form is recommended so signals (e.g. SIGTERM) go to the process, not a shell.

Only **one `CMD`** is used per stage; if you write multiple, **only the last one** applies. Override at run time with a command after the image: `docker run my-hello sh`.

**Where does CMD come from?** You write it in the Dockerfile. The **Docker daemon** interprets it (build/run). **Alpine** doesn’t provide CMD; it only provides the filesystem and programs like `echo`.

---

## Multiple lines in one CMD?

One `CMD` = one process. To echo multiple lines:

- **`printf`:** `CMD ["printf", "line1\nline2\n"]` (Alpine has `printf`).
- **Shell:** `CMD sh -c 'echo "line1"; echo "line2"'`.
- Or put commands in a script and `CMD ["/script.sh"]`.

---

## What does `-t` in `docker build` do?

**`-t`** = **`--tag`**. It gives the built image a **name** (and optional tag).

- `docker build -t my-hello .` → image tagged **`my-hello:latest`**.
- `docker build -t my-hello:1.0 .` → image tagged **`my-hello:1.0`**.

So you can run `docker run my-hello` instead of using the image ID. **Tag belongs to the image**, not the container (containers have names/IDs).

---

## What is the `.` in `docker build`?

**`.`** = **build context** = the **current working directory** of your shell (“where” you are when you run the command).

- Docker looks for the Dockerfile and any files for `COPY` **relative to this directory**.
- **`.`** = where to **read from** (input). The image is **saved** in Docker’s storage (e.g. `/var/lib/docker/`), which you don’t set with `.` — that’s automatic.

---

## Which Dockerfile does Docker read?

**Default:** A file named exactly **`Dockerfile`** (capital D) at the **root of the build context**. No other name is used unless you specify it.

**Multiple or different names:** Use **`-f`** to choose the file:

- `docker build -f dockerfile1 -t myimage1 .`
- `docker build -f dockerfile2 -t myimage2 .`
- `docker build -f path/to/Dockerfile.prod -t myimage .`

**`-f`** = path to the file to use as the Dockerfile; it can be **any filename or path** (not only `Dockerfile`). If you have only `dockerfile1` and `dockerfile2`, you **must** use `-f`; the default `Dockerfile` won’t exist.

---

## Where is the image saved?

The image is stored in **Docker’s local storage** (e.g. **`/var/lib/docker/`** on Linux), not as a single file. You use it via `docker run <tag>` and `docker images`. The “naming to …” and “unpacking to …” in the build output refer to that storage and the tag (e.g. `alpine-echo-cmd:latest`).

---

## Build warnings (multiple CMD, JSON recommended)

- **Multiple CMD:** Only the **last** `CMD` in a stage is used; remove the others.
- **JSON args recommended:** Use the **exec form** `CMD ["echo", "Hello!"]` instead of the shell form so the process gets signals correctly (e.g. `docker stop`).
