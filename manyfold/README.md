# Manyfold

Manyfold is a self-hosted application for managing and organizing 3D models.

## Purpose

This Docker Compose stack deploys Manyfold, a self-hosted application for managing and organizing 3D models.

## What This Stack Includes

-   `app`: The Manyfold application server.
-   `postgres`: A PostgreSQL database for Manyfold's data persistence.
-   `redis`: A Redis server for caching and background jobs.

## Configuration Overview

Sensitive credentials and cryptographic keys are managed via a `.env` file to separate them from the `docker-compose.yml`.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

1.  Create a `.env` file in the same directory as your `docker-compose.yml` with the following content:

    ```ini
    SECRET_KEY_BASE=a_nice_long_random_string
    DATABASE_USER=manyfold_user
    DATABASE_PASWORD=secure-password-here
    ```

    *   Replace `a_nice_long_random_string` with a unique, randomly generated string for `SECRET_KEY_BASE`.
    *   Adjust `DATABASE_USER` and `DATABASE_PASWORD` as needed.

2.  Deploy the stack:

    ```bash
    docker compose up -d
    ```

3.  Access the Manyfold web interface at `http://localhost:3214` (or your host's IP address).

## Operational Notes

*   Database persistence is handled by the `db_data` Docker volume.
*   To store your 3D model libraries persistently, uncomment and configure the `volumes` section for the `app` service, mapping a local path to a container path (e.g., `- /local/path/to/your/models:/models`).
*   Adjust `PUID` and `PGID` environment variables for the `app` service to match the user/group ID that should own the application files within the container, especially if mounting local model library volumes.
*   The provided `DATABASE_USER` and `DATABASE_PASWORD` in the `.env` file must match the `POSTGRES_USER` and `POSTGRES_PASSWORD` configured for the `postgres` service. By default, the `postgres` service uses `manyfold` and `password`. Update the `.env` file or the `postgres` service configuration accordingly.

## Known Limitations

*   The `postgres` service in this stack uses hardcoded `POSTGRES_USER` and `POSTGRES_PASSWORD` values that may not match the credentials defined in your `.env` file for the `app` service. This requires manual adjustment to ensure connectivity.

## Upstream Project

-   Website: https://manyfold.app
-   GitHub: https://github.com/manyfold3d/manyfold

## Final Notes

This stack provides a robust base for deploying Manyfold. Adapt it as required for specific use cases.
