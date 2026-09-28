# ZuriHost — Ubuntu SSH Cloud Server

Ubuntu 24.04 + OpenSSH server image that ZuriHost provisions to give
each customer a ready-to-use cloud server, reachable over SSH on port 22.

Website: **https://zurihost.biz.id**

## What's inside

- Ubuntu 24.04 base with `sshd` (root login enabled, password auth).
- A full cloud-workstation toolkit (git, build tools, Python, Node.js, editors,
  monitoring, archivers, networking utilities).
- Claude Code CLI pre-installed (`cl` opens it in a tmux session).
- A branded ZuriHost login banner (`/etc/profile.d/zuri-welcome.sh`).
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

The image is built from its `Dockerfile`. The start command
(`ssh-user-config.sh`) applies the runtime password/keys and launches `sshd`.
