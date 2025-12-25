# Blinko

A Docker Compose stack for deploying Blinko, a collaborative workspace platform.

## Purpose

This stack provides a self-contained Docker Compose deployment for Blinko, including its web application and PostgreSQL database.

## What This Stack Includes

-   **blinko-website**: The main Blinko web application, served via Node.js.
-   **postgres**: A PostgreSQL 14 database instance for Blinko data.

## Configuration Overview

Configuration relies on a `.env` file for sensitive data and deployment-specific values. This approach separates secrets from the Compose file and facilitates environment-specific adjustments.

Sensitive values such as `NEXTAUTH_SECRET` and `POSTGRES_PASSWORD` must be set in the `.env` file. The `NEXTAUTH_URL` and `NEXT_PUBLIC_BASE_URL` should be configured to match the intended external access URL.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

1.  Copy `.env.example` to `.env` and populate all variables with appropriate values.
2.  From the directory containing `docker-compose.yml` and `.env`, execute:
    ```bash
    docker compose up -d
    ```
3.  Access the web UI at the address configured in `NEXTAUTH_URL`, e.g., `http://localhost:1111`.

## Operational Notes

-   Application data persists to `./data/app` and database data to `./data/db` relative to the `docker-compose.yml` file. Ensure appropriate permissions are set for these directories.
-   Health checks are configured for both `blinko-website` and `postgres` to ensure service readiness and dependency satisfaction.
-   The `NEXTAUTH_SECRET` variable is critical for session security and must be a strong, randomly generated value.

## Known Limitations

-   The default `.env` provided uses placeholder values for `NEXTAUTH_SECRET` and `POSTGRES_PASSWORD`. These must be replaced with secure, randomly generated values before deployment.
-   The `NEXTAUTH_URL` and `NEXT_PUBLIC_BASE_URL` in the example `.env` are set to `http://localhost:1111`, which is suitable only for local development or testing. These must be updated to the actual public URL of your Blinko instance for proper operation, especially if using SSO features.

## Upstream Project

-   Website: [https://blinko.space/](https://blinko.space/)
-   GitHub: [https://github.com/blinkospace/blinko](https://github.com/blinkospace/blinko)

## Final Notes

This stack provides a robust foundation for Blinko deployments. Review and adjust configuration to meet specific security and operational requirements.
