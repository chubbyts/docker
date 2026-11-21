# docker

## Setup on host

### Environment

Add the following environment variable to your system, for example within `~/.bashrc` or  `~/.zshrc`:

```sh
export USER_ID=$(id -u)
export GROUP_ID=$(id -g)
```

### Mount points

Creates every file and directory which gets mounted into the node container without overwriting existing ones:

 * shell rc/history, git, ssh and npm files within the host home (`~`)
 * coding agent directories within `.home` (within this repository, git-ignored), seeded with default settings

Adjust the seeded settings files afterwards to your liking, they stay on the host and get mounted.

```sh
./setup-mount-points.sh
```

### Coding agents

The following coding agents (harnesses) are preinstalled within the node container, their directories get mounted
from `.home` (see `docker-compose.yml`), so auth, settings, sessions and history survive container rebuilds:

 * [Claude Code](https://www.npmjs.com/package/@anthropic-ai/claude-code)
 * [Codex](https://www.npmjs.com/package/@openai/codex)
 * [Gemini CLI](https://www.npmjs.com/package/@google/gemini-cli)
 * [Opencode](https://www.npmjs.com/package/opencode-ai)
 * [PI](https://www.npmjs.com/package/@earendil-works/pi-coding-agent) incl. [pi-llama](https://github.com/huggingface/pi-llama) (installed on first start)

Use `claude-reset`, `codex-reset`, `gemini-reset`, `opencode-reset`, `pi-reset` or `harness-reset` within the
container to wipe the agent state while keeping auth and settings.

#### llama.cpp

PI can run against a local model via [pi-llama](https://github.com/huggingface/pi-llama), start a
[llama.cpp](https://llama.app/) server on the host, for example:

```sh
llama-server \
    -hf lmstudio-community/Qwen3.6-35B-A3B-GGUF:Q4_K_M \
    -c 32768 \
    -ngl 999 \
    --flash-attn on \
    --host 0.0.0.0 \
    --port 9931
```

### Docker

```sh
docker compose up -d
docker compose exec node bash
```

##  Use nginx as reverse proxy

**IMPORTANT: It is meant for simple testing a project not having an own docker setup yet.**

Nginx is configured to reverse proxy to port 3000.

To you use run an app with host 0.0.0.0 and port 3000.

On your host call it via

```sh
curl --insecure https://localhost/path/to/route
```

## Copyright

2026 Dominik Zogg
