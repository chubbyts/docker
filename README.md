# docker

## setup on host

### bash

```sh
touch ~/.bash_docker
touch ~/.bash_history
```

### git

```sh
touch ~/.gitconfig
touch ~/.gitignore
```

### npm

```sh
touch ~/.npmrc
```

### opencode

```sh
mkdir -p ~/.local/share/opencode
[ ! -f ~/.local/share/opencode/auth.json ] && echo '{}' > ~/.local/share/opencode/auth.json
```

### ssh

```sh
mkdir -p ~/.ssh
touch github.pub
```

### zsh

```sh
touch ~/.zsh_docker
touch ~/.zsh_history
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
