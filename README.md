# docker

## setup on host

### bash

```sh
touch ~/.bash_docker
touch ~/.bash_history
```

### zsh

```sh
touch ~/.zsh_docker
touch ~/.zsh_history
```

### git

```sh
touch ~/.gitconfig
touch ~/.gitignore
```

### ssh

```sh
mkdir -p ~/.ssh
touch github.pub
```

### npm

```sh
touch ~/.npmrc
```

### Coding agents

#### Claude

```sh
if [ ! -f ~/.claude.json ]; then
    cat > ~/.claude.json <<'EOF'
{}
EOF
fi

mkdir -p ~/.claude

if [ ! -f ~/.claude/.credentials.json ]; then
    cat > ~/.claude/.credentials.json <<'EOF'
{}
EOF
fi

if [ ! -f ~/.claude/settings.json ]; then
    cat > ~/.claude/settings.json <<'EOF'
{
    "fileCheckpointingEnabled": false,
    "permissions": {
        "defaultMode": "bypassPermissions"
    },
    "skipDangerousModePermissionPrompt": true,
    "spinnerTipsEnabled": false,
    "switchModelsOnFlag": false,
    "theme": "auto"
}
EOF
fi

chmod 600 \
    ~/.claude/.credentials.json \
    ~/.claude/settings.json
```

#### Codex

```sh
mkdir -p ~/.codex

if [ ! -f ~/.codex/auth.json ]; then
    cat > ~/.codex/auth.json <<'EOF'
{}
EOF
fi

if [ ! -f ~/.codex/config.toml ]; then
    cat > ~/.codex/config.toml <<'EOF'
approval_policy = "never"
sandbox_mode = "danger-full-access"

[notice]
hide_full_access_warning = true
EOF
fi

chmod 600 \
    ~/.codex/auth.json
    ~/.codex/config.toml
```

#### Opencode

```sh
mkdir -p ~/.config/opencode ~/.local/share/opencode

if [ ! -f ~/.config/opencode/opencode.jsonc ]; then
    cat > ~/.config/opencode/opencode.jsonc <<'EOF'
{
    "$schema": "https://opencode.ai/config.json",
    "permission": {
        "*": "allow"
    }
}
EOF
fi

if [ ! -f ~/.config/opencode/tui.json ]; then
    cat > ~/.config/opencode/tui.json <<'EOF'
{
    "$schema": "https://opencode.ai/tui.json",
    "theme": "system",
    "tips": false
}
EOF
fi

if [ ! -f ~/.local/share/opencode/auth.json ]; then
    printf '{}\n' > ~/.local/share/opencode/auth.json
fi

chmod 600 \
    ~/.config/opencode/opencode.jsonc \
    ~/.config/opencode/tui.json \
    ~/.local/share/opencode/auth.json
```

#### PI

```sh
mkdir -p ~/.pi/agent
[ ! -f ~/.pi/agent/auth.json ] && echo '{}' > ~/.pi/agent/auth.json
```

##### llama.cpp

```sh
llama-server -hf lmstudio-community/Qwen3.6-35B-A3B-GGUF:Q4_K_M -c 32768 -ngl 999 --flash-attn on --host 0.0.0.0 --port 9931
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
