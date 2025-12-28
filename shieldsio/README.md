# Shields.io

A service for creating SVG badges for open-source projects.

## Purpose

This stack provides a self-hosted instance of Shields.io, enabling custom badge generation and reducing reliance on the public service's GitHub API rate limits.

## What This Stack Includes

-   The `shieldsio/shields:next` Docker image, running the Shields.io badge server.

## Configuration Overview

Sensitive values are managed via a `.env` file to prevent their exposure in version control. The included `docker-compose.yml` references these variables.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

1.  Create a `.env` file in the same directory as the `docker-compose.yml`. Populate it with the necessary variables, such as `GH_TOKEN` for GitHub API access. A `GH_TOKEN` is recommended to avoid low API rate limits.
    ```
    GH_TOKEN=your_github_personal_access_token
    BASE_URL=https://your.custom.domain
    ```
2.  Start the stack:
    ```bash
    docker compose up -d
    ```
3.  The service will be available on port `7080`.

## Operational Notes

Ensure the `BASE_URL` environment variable is correctly configured to reflect the domain where your Shields.io instance will be publicly accessible. Incorrect configuration will lead to broken badge URLs. Using a `GH_TOKEN` significantly increases the GitHub API rate limit, preventing service interruptions for projects with many GitHub-related badges.

## Known Limitations

Self-hosting Shields.io means you are responsible for its uptime and performance. It will not benefit from the global CDN infrastructure that the public Shields.io service utilizes.

## Upstream Project

-   Website: [shields.io](https://shields.io/)
-   GitHub: [https://github.com/badges/shields](https://github.com/badges/shields)

## Final Notes

Self-hosting Shields.io provides control over badge content and API usage, but requires careful configuration of its base URL and API tokens.
