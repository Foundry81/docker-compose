# Backrest
A Docker Compose stack for running Backrest, a tool for backing up Docker volumes and local paths.

## Purpose
This stack provides a pre-configured Docker Compose setup for Backrest. It enables persistent storage for Backrest's operational data and defines the necessary volumes for Docker socket access and backup targets.

## What This Stack Includes
- `backrest` service based on `garethgeorge/backrest`.
- Persistent storage for Backrest data (`./data`), configuration (`./config`), cache (`./backrest/cache`), and temporary files (`./backrest/tmp`).
- Read-only access to `/var/run/docker.sock` for Docker volume discovery.
- An example mount for local paths intended for backup (`/storage/docker`).
- Web UI exposed on port `9132`.

### Configuration Overview
All configuration is inline within `docker-compose.yml`. No `.env` file is required as no sensitive values are present.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
1. Ensure Docker and Docker Compose are installed.
2. Clone this repository or copy the `docker-compose.yml` file.
3. Adjust the volume mounts in `docker-compose.yml` to reflect your desired backup sources and destinations.
4. Run the stack: `docker compose up -d`
5. The web UI is available on port `9132`.

## Docker Socket Notes
This stack mounts `/var/run/docker.sock` into the `backrest` container. This grants the container the same level of access to your Docker daemon as the host machine itself. Ensure you understand the security implications before deploying this stack.

## Operational Notes
- The `TZ` environment variable is set to `America/New_York`. Adjust this to your local timezone as needed.
- Customize the `/storage/docker` volume mount to point to the specific paths you intend to back up.
- Consider adding explicit volume mounts for backup repositories (e.g., `#/path-to/backups`) if you are not using remote storage for backups.
- Similarly, define a mount for restore operations (e.g., `#/path-to/restores:/restores`) if you need to access restored content directly from the host.
 
## Known Limitations
- Requires direct access to the Docker socket for volume discovery.
- The provided Compose file does not include explicit local mounts for backup destinations, assuming remote storage or user-defined modifications.

## Upstream Project
- GitHub: [https://github.com/garethgeorge/backrest](https://github.com/garethgeorge/backrest)

## Final Notes
This setup provides a functional Backrest instance. Configure it according to your specific backup requirements.

