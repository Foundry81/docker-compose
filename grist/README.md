# Grist
Grist is a modern, open-source spreadsheet with relational database capabilities.
## Purpose
This stack provides a self-hosted instance of Grist via Docker Compose.
## What This Stack Includes
- `gristlabs/grist` application service
- A persistent volume for application data at `./data:/persist`
## Configuration Overview
Configuration is handled inline within the `docker-compose.yml` file. An `.env` file is not used as there are no sensitive values or frequently customized parameters in this minimal setup.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.
## Usage
To start the Grist stack:
```bash
docker compose up -d
```
The web UI will be available on `http://localhost:8484`.
## Operational Notes
Application data is persisted to the `./data` directory on the host. This directory must be backed up to ensure data integrity.
## Known Limitations
This stack provides a basic, single-instance deployment of Grist. It does not include advanced features like high availability, load balancing, or a dedicated database service, which may be required for production environments.
## Upstream Project
- Website: https://www.gristlabs.com/
- GitHub: https://github.com/gristlabs/grist-core
## Final Notes
This stack offers a straightforward path to deploying Grist for personal or small-team use.

