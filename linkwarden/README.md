# Linkwarden

A self-hosted bookmark and link management system.

## Purpose

To provide a simple, self-contained Docker Compose stack for deploying Linkwarden with its PostgreSQL and MeiliSearch dependencies.

## What This Stack Includes

-   Linkwarden (the application)
-   PostgreSQL (database backend)
-   MeiliSearch (search engine for indexing links)

## Configuration Overview

Sensitive variables such as `NEXTAUTH_SECRET`, `MEILI_MASTER_KEY`, and `POSTGRES_PASSWORD`, along with the `NEXTAUTH_URL`, are externalized into a `.env` file. This allows for secure storage of credentials and easy modification of deployment-specific settings without altering the `compose.yaml`. Replace placeholder values with strong, unique secrets before deployment.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

1.  Copy `.env.example` to `.env`:
    ```bash
    cp .env.example .env
    ```
2.  Edit the `.env` file and replace all placeholder values with strong, unique secrets and your desired `NEXTAUTH_URL`.
3.  Start the stack:
    ```bash
    docker compose up -d
    ```
4.  Access the web UI via your configured reverse proxy or directly at `http://localhost:3000`.

## Operational Notes

-   Persistent data for Linkwarden, PostgreSQL, and MeiliSearch is stored in `./data`, `./pgdata`, and `./meili_data` respectively.
-   Ensure `NEXTAUTH_SECRET` is a long, random string to protect user sessions.
-   Configure `NEXTAUTH_URL` to match the public-facing URL of your Linkwarden instance, including the protocol (e.g., `https://your.domain.com`).
-   An initial administrator user must be created via the Linkwarden web interface upon first access.

## Known Limitations

-   This stack is designed for single-node deployments. Scaling beyond a single instance requires additional configuration not provided here.

## Upstream Project

-   Website: [https://linkwarden.app/](https://linkwarden.app/)
-   GitHub: [https://github.com/linkwarden/linkwarden](https://github.com/linkwarden/linkwarden)

## Final Notes

This stack provides a robust foundation for self-hosting Linkwarden. Review all configurations for security and performance before exposing to untrusted networks.
