# BentoPDF

A Docker Compose stack for running BentoPDF, a lightweight PDF rendering service.

## Purpose

To provide a self-contained, simple deployment of the BentoPDF service for generating PDFs from URLs or HTML.

## What This Stack Includes

- The `bentopdf/bentopdf-simple:latest` Docker image.

## Configuration Overview

This stack does not require a `.env` file. All necessary configuration is defined inline within the `docker-compose.yml` file.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

Start the stack:

```bash
docker compose up -d
```

The BentoPDF service will be available at `http://localhost:8080`. Refer to the BentoPDF documentation for API usage.

## Operational Notes

- This stack uses the `bentopdf/bentopdf-simple` image, which is optimized for basic PDF rendering. Consider the `bentopdf/bentopdf` image for more advanced features if required.
- Monitor container logs for service status and rendering issues.

## Known Limitations

- The `simple` mode of BentoPDF may lack advanced features available in the default image.
- Performance characteristics for high-volume PDF generation should be evaluated based on specific use cases.

## Upstream Project

- GitHub: https://github.com/alam00000/bentopdf
- Website: https://www.bentopdf.com/

## Final Notes

This stack provides a robust foundation for integrating PDF generation into your services.

