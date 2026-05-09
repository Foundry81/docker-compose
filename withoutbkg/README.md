# withoutBG

A self-hosted service for automated background removal from images.

## Purpose

Provides a containerized instance of the withoutBG background removal engine for local or private image processing workflows.

## What This Stack Includes

- withoutbg: The core application container handling image processing tasks.

## Configuration Overview

No .env file is required as there are no sensitive credentials or persistent external service keys defined in the base configuration. All ports and service settings are managed inline within the compose file.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

Start the stack:
```bash
docker compose up -d
```

Access the web interface at `http://localhost:8080`.

## Operational Notes

- The service is resource-intensive due to image processing requirements; ensure the host machine has sufficient CPU and RAM.
- No persistent storage is defined in the initial configuration; files uploaded to the instance will be cleared upon container recreation. If persistence is required, map a local directory to the container's output volume.

## Known Limitations

- The default image lacks GPU acceleration support. Expect some latency during processing on large batches or high-resolution images.
- The service exposes an unauthenticated web UI; ensure it is placed behind an identity-aware proxy or VPN when deployed on a network.

## Upstream Project

- Website: https://withoutbg.com/

## Final Notes

Simple, single-purpose tool. Do not expose directly to the public internet without an authentication layer.
