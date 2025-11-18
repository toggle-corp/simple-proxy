# Simple Proxy

A simple proxy server using Caddy.

## Usage

We will use `idmc` as the example project name.
Our project will needs these files:

```bash
├── config
│   └── caddy
│       └── projects
│           └── idmc.caddy
└── compose
    └── idmc.yml
```

**config/caddy/projects/idmc.caddy**

```caddy
import /etc/caddy/snippets/proxy.caddy

http://localhost:8001 {
    import reverse_proxy helix-tools-api-staging.idmcdb.org
}
```

**compose/idmc.yml**

```yaml
services:
  caddy:
    environment:
      PROJECT_NAME: idmc
    ports:
      - 8001:8001
```

To start the proxy server, run:

```bash
docker compose -f docker-compose.yml -f compose/idmc.yml up
```
