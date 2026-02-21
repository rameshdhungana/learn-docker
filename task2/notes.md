# Task 2 — Notes: Interactive containers

Summary of what we learned while completing Task 2.

---

## Why didn’t interactive “open” with hello-world?

**The `hello-world` image doesn’t run a shell — it runs a small program that prints a message and exits.**

What happens:

1. You run `docker run -it hello-world`.
2. Docker starts the container with a TTY (`-it`).
3. The image’s default program runs (the hello-world binary).
4. That program prints “Hello from Docker!” and exits.
5. When the main process exits, the **container stops**. You’re back at your host shell — no prompt inside the container.

So you never get an interactive prompt because nothing is waiting for your input; the only process is the hello-world binary, and it just prints and exits.

**To get a real interactive session**, use an image that runs a **shell** (a process that stays running and reads input):

```bash
sudo docker run -it ubuntu bash
```

- **`ubuntu`** = image that has a shell
- **`bash`** = command run inside the container (interactive shell)
- The shell keeps the container alive and gives you a prompt. Then you can run `cat /etc/os-release` and `exit`.

**Summary:** With `hello-world`, the program inside didn’t wait for input — it printed and exited. Use `docker run -it ubuntu bash` (or `alpine` with `sh`) for an actual interactive shell.

---

## Argument order matters

Options like `-it` must come **before** the image name:

- **Wrong:** `docker run hello-world -it` → Docker treats `-it` as the **command** to run inside the container (a program named "-it"), so you get “executable file not found”.
- **Right:** `docker run -it hello-world` or `docker run -it ubuntu bash`

Order: **`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`**
