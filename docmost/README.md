# Docmost
A self-hosted document management system.

## Purpose
This stack provides a Docmost instance, complete with its database and Redis backend, suitable for personal or small team deployments.

## What This Stack Includes
- **Docmost Application:** The main Docmost web service.
- **PostgreSQL:** Database for Docmost data.
- **Redis:** Cache and job queue for Docmost.

### Configuration Overview
Sensitive credentials and application-specific settings are managed via the `.env` file. This prevents hardcoding secrets in `docker-compose.yml` and facilitates easier environment-specific adjustments.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
Create a `.env` file based on the provided `docker.env` example.
Fill in all `replace-with-a-secure-random-string` or `replace-with-a-strong-db-password` placeholders with strong, unique values.
Adjust `APP_URL` to reflect the public URL where Docmost will be accessed.

Start the stack:
```bash
docker compose up -d
```
The Docmost web UI will be available on port `3300`.

## Operational Notes
- Application data is stored in the `./storage` directory.
- PostgreSQL data is persisted in the `./data` directory.
- Redis data is persisted in the `./redis` directory.
- Ensure the `APP_URL` in your `.env` file accurately reflects how users will access the application to avoid potential redirect or asset loading issues.

### Known Limitations
- This stack is configured for a single-node deployment.
- Database and Redis instances are co-located with the application. For production environments requiring high availability or scaling, consider external, managed database and Redis services.
 
## Upstream Project
- GitHub: https://github.com/docmost/docmost
- Website: https://docmost.com

## Final Notes
This Compose stack provides a functional Docmost setup. Adapt it to your specific infrastructure requirements.

