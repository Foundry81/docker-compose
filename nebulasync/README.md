# nebula-sync

Synchronizes Nebula network configuration across multiple hosts.

## Purpose

Provides a self-contained environment to run the `nebula-sync` tool for maintaining Nebula network consistency.

## What This Stack Includes

- `nebula-sync`: The synchronization service using `ghcr.io/lovelaze/nebula-sync`.

## Configuration Overview

This stack uses a `.env` file for sensitive values. The `PRIMARY` and `REPLICAS` variables contain host IP addresses and API passwords. Storing these values in environment variables rather than directly in `docker-compose.yml` avoids committing credentials to version control.

## Usage

1.  Create a `.env` file from the example:
    ```bash
    cp .env.example .env
    ```
2.  Edit the `.env` file with your specific `PRIMARY` and `REPLICAS` details, including API passwords.
3.  Start the service:
    ```bash
    docker compose up -d
    ```

This service operates in the background, performing scheduled synchronizations. Output can be monitored via `docker compose logs -f nebula-sync`.

## Operational Notes

The `nebula-sync` service runs on a schedule defined by the `CRON` environment variable, configured for every 15 minutes by default. It performs a full synchronization (`FULL_SYNC=true`) and runs Gravity (`RUN_GRAVITY=true`) on each cycle. Ensure that `nebula-sync` can reach the specified primary and replica hosts over the network, and that the provided API passwords are correct.

## Known Limitations

This tool relies on direct API access to your Nebula nodes. This requires careful management of API passwords and network access permissions for the `nebula-sync` container.

## Upstream Project

- GitHub: [https://github.com/lovelaze/nebula-sync](https://github.com/lovelaze/nebula-sync)

## Final Notes

This stack offers a straightforward method for deploying `nebula-sync`. Adapt its configuration to fit your network synchronization requirements.

