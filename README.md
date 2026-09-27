# ZuriHost — Railway Ubuntu SSH VPS

Ubuntu 24.04 + OpenSSH server image that ZuriHost deploys on Railway to give
each customer a ready-to-use cloud VPS, reachable over SSH via a Railway TCP
proxy on port 22.

Website: **https://zurihost.biz.id**

## What's inside

- Ubuntu 24.04 base with `sshd` (root login enabled, password auth).
- A full cloud-workstation toolkit (git, build tools, Python, Node.js, editors,
  monitoring, archivers, networking utilities).
- Claude Code CLI pre-installed (`cl` opens it in a tmux session).
- A branded ZuriHost login banner (`/etc/profile.d/zuri-welcome.sh`).
- `usage` — Railway trial credit + uptime monitor.
- `src-sync` — optional `/root/src` ⇄ private GitHub backup.

## Runtime environment variables

| Variable                | Required | Purpose                                             |
| ----------------------- | -------- | --------------------------------------------------- |
| `ROOT_PASSWORD`         | **yes**  | Root SSH password. Container refuses to start w/o it.|
| `SSH_USERNAME` / `SSH_PASSWORD` | no | Optional secondary sudo user.                   |
| `AUTHORIZED_KEYS`       | no       | Public key(s) for key-based login.                  |
| `ANTHROPIC_AUTH_TOKEN`  | no       | Enables Claude Code.                                 |
| `GITHUB_TOKEN`          | no       | Enables `src-sync` auto-backup.                     |

See [TOKENS.md](TOKENS.md) for token details.

## Build

Railway builds this repo from its `Dockerfile` (`railway.json` declares the
Dockerfile builder). The start command (`ssh-user-config.sh`) applies the
runtime password/keys and launches `sshd`.
