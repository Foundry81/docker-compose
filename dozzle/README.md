# Dozzle
A real-time log viewer for Docker containers.
## Purpose

This stack provides a web-based interface for viewing Docker container logs, useful for local development and debugging

## What This Stack Includes
-   `dozzle`: The Dozzle container, configured to access the Docker host's socket for log retrieval.
## Configuration Overview
All configuration is handled inline within the `docker-compose.yml` file. No sensitive values are present, so a `.env` file is not required.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
To start the Dozzle service:
```bash
docker compose up -d
```
Access the web interface at `http://localhost:8080`.

## Docker Socket Notes
Mounting `/var/run/docker.sock` into a container grants that container the same level of access as the Docker daemon itself. This is a significant security risk. Only use this setup in trusted environments with trusted containers.
## Operational Notes
Dozzle provides a live stream of container logs, making it suitable for active monitoring and troubleshooting without needing to access container internals or the host directly.
## Known Limitations
Direct access to the Docker socket means the Dozzle container has elevated privileges on the Docker host.
## Upstream Project
-   GitHub: [https://github.com/amir20/dozzle](https://github.com/amir20/dozzle)

## Final Notes
Dozzle offers a straightforward and effective way to gain immediate insight into container activity.
