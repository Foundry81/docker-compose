# convert-svg-to-png-docker

A Docker Compose stack providing a web service for converting SVG images to PNG.

## Purpose

Provides a portable, stateless web service for converting SVG images to PNG using the `pluswerk/convert-svg-to-png` Docker image.

## What This Stack Includes

-   `svg-renderer` service based on `pluswerk/convert-svg-to-png`.
-   Exposes port `3000` internally, mapped to `8999` externally.

## Configuration Overview

All configuration is inline within the `docker-compose.yml` file. No `.env` file is required as there are no sensitive or variable values.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

To start the service:

```bash
docker compose up -d
```

Once the stack is running, access the conversion service via `http://localhost:8999` or `http://your-host-ip:8999`. Refer to the upstream project documentation for API specifics.

## Operational Notes

This service is stateless and does not persist any data. It is suitable for on-demand conversions or integration into internal tools.

## Known Limitations

The service is stateless; no conversion history or configuration is persisted across restarts.

## Upstream Project

-   GitHub: [https://github.com/pluswerk/docker-convert-svg-to-png](https://github.com/pluswerk/docker-convert-svg-to-png)

## Final Notes

This stack provides a straightforward method for on-demand SVG to PNG conversion.
