# n8n

n8n is a fair-code licensed workflow automation platform.

## Purpose

This stack provisions n8n with dedicated database and queue services, configured for external execution and scalability.

## What This Stack Includes

-   `n8n`: The main web service for the n8n UI and API.
-   `n8n-worker`: A dedicated n8n process for background task processing.
-   `n8n-runners-main` and `n8n-runners-worker`: External runner services for workflow execution.
-   `postgres`: A PostgreSQL database backend for persistent data storage.
-   `redis`: A Redis instance for the workflow queue and caching.

## Configuration Overview

Sensitive variables, such as database credentials, the n8n encryption key, and runner authentication token, are managed via the `.env` file. Modify the example values for your deployment.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

Deploy the stack:

```bash
docker compose up -d
```

Access n8n via the hostname configured in the `N8N_HOST` variable in your `.env` file, after setting up a reverse proxy. For example, `https://n8n.example.com`.

## Operational Notes

-   This stack utilizes an external PostgreSQL database and Redis queue, which is recommended for production n8n deployments for performance and reliability.
-   Workflow executions are offloaded to dedicated `n8n-worker` and `n8n-runners` services. This enables horizontal scaling of execution capacity and isolates the main web service.
-   Persistent data is stored in named volumes for the database (`db_storage`), Redis (`redis_storage`), and n8n application data (`n8n_storage`, `n8n-files`).
-   The PostgreSQL setup includes `POSTGRES_NON_ROOT_USER` and `POSTGRES_NON_ROOT_PASSWORD` variables to create a dedicated user for n8n, enhancing database security.

## Known Limitations

-   The provided `init-data.sh` script for PostgreSQL is currently empty. Custom database initialization or seeding requires modifying this file.

## Upstream Project

-   Website: [https://n8n.io](https://n8n.io)
-   GitHub: [https://github.com/n8n-io/n8n](https://github.com/n8n-io/n8n)

## Final Notes

This stack provides a robust foundation for n8n deployments. Adapt the resource allocation and scaling to match your specific workflow demands.
