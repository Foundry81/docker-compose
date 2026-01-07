# Dockge

Dockge provides a web-based interface for managing Docker Compose stacks.

## Purpose

This stack provides a convenient web UI for creating, editing, and deploying Docker Compose projects directly on a Docker host.

## What This Stack Includes

-   `dockge` service, running `louislam/dockge:1`
-   Exposed port `5001` for the web UI
-   Access to the Docker socket (`/var/run/docker.sock`) for container and stack management
-   Persistent data storage for Dockge's configuration and logs in `./data`
-   A dedicated directory (`/opt/stacks`) for Docker Compose stack files, managed by Dockge
-   Environment configuration to enable the web console (`DOCKGE_ENABLE_CONSOLE=true`)

## Configuration Overview

This stack uses inline configuration within the `docker-compose.yml` file. No sensitive variables are present, thus a `.env` file is not required.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

Deploy the stack:

```bash
docker compose up -d
```

Access the web UI at `http://localhost:5001` (replace `localhost` with your host's IP if not accessing from the host directly).

## Docker Socket Notes

This stack mounts `/var/run/docker.sock` into the `dockge` container. This grants the container the same level of access to your Docker daemon as the Docker client itself, effectively providing root-level access to your host system. Exercise extreme caution.

## Operational Notes

-   The `DOCKGE_STACKS_DIR` environment variable is explicitly set to `/opt/stacks` and must match the host path of the corresponding volume mount for stack management to function correctly.
-   If Dockge needs to interact with private Docker registries, uncomment and configure the `/root/.docker:/root/.docker` volume mount in `docker-compose.yml`. Ensure the Docker configuration file (`config.json`) with registry authentication is present on the host at `/root/.docker/config.json`.

## Known Limitations

-   Direct Docker socket access gives Dockge full control over the Docker daemon. A compromise of the Dockge interface could lead to a compromise of the host system.
-   While convenient, a web interface may not offer the full flexibility or scripting capabilities for advanced Docker Compose operations compared to direct CLI interaction.

## Upstream Project

-   GitHub: [https://github.com/louislam/dockge](https://github.com/louislam/dockge)

## Final Notes

Prioritize security when exposing management interfaces with elevated privileges.

