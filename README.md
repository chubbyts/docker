# docker

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
