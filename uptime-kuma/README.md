# Uptime Kuma
A self-hosted monitoring tool.
## Purpose
This stack provides an easy-to-deploy instance of Uptime Kuma for self-hosted status monitoring.
## What This Stack Includes
- `uptime-kuma` service container
- Persistent data storage for application data
- Docker socket mount for host container monitoring
- Web UI exposed on port 3001
## Configuration Overview
- This stack is configured entirely inline within the `docker-compose.yml` file. No `.env` file is required, as there are no sensitive values to manage.
- The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.
## Usage
To deploy this stack:
```bash
docker compose up -d
```
Access the Uptime Kuma web UI via your reverse proxy, or directly at `http://localhost:3001` if no proxy is configured.
## Docker Socket Notes
The `uptime-kuma` service mounts `/var/run/docker.sock` from the host. This grants the container the ability to interact with the Docker daemon, effectively providing root-level access to the host. Review the implications before deployment.
## Operational Notes
Upon first access, an administrative user account must be created through the web UI.
## Known Limitations
This stack uses the `nightly2` image tag, which may introduce instability or breaking changes compared to stable releases.
## Upstream Project
-   GitHub: [https://github.com/louislam/uptime-kuma](https://github.com/louislam/uptime-kuma)
## Final Notes
Self-hosting monitoring tools requires thoughtful configuration for reliability.

