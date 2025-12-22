# Twenty
Open-source CRM platform.

## Purpose
Provides a self-hosted instance of the Twenty open-source CRM platform.

## What This Stack Includes
- Twenty application server with web UI.
- Twenty background worker.
- PostgreSQL database for persistent data.
- Redis for caching and message queuing.

## Configuration Overview
Sensitive values such as database credentials and the application secret are managed via a `.env` file. Other configuration can be set inline or also moved to `.env`.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
Deploy the stack:
```bash
docker compose up -d
```
Access the Twenty web UI on port 3000 of the Docker host.

## Operational Notes
- The `APP_SECRET` must be set to a strong, random value. Use `openssl rand -base64 32` to generate a suitable string.
- The `SERVER_URL` variable should reflect the publicly accessible URL of your Twenty instance for proper link generation and callback URLs.
- Default storage is local, persisting to `./server-local-data`. For scalable deployments, consider configuring S3 storage via the `STORAGE_TYPE` and related S3 environment variables.

## Known Limitations
- This configuration uses local file storage, which is not suitable for horizontally scaled or highly available deployments.
- Advanced features like email sending, external authentication (Google, Microsoft), and calendar integrations are not configured by default and require additional environment variables.

## Upstream Project
- Website: https://www.twenty.com
- GitHub: https://github.com/twentyhq/twenty

## Final Notes
This stack provides a functional Twenty instance for evaluation or controlled environments.
