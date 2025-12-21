# Quickchart
A self-hosted service for generating chart images via an API.
## Purpose
This stack provides a local instance of Quickchart for programmatic chart generation.
## What This Stack Includes
- The `quickchart` service, exposing the Quickchart API.
### Configuration Overview
This stack uses inline Docker Compose configuration. No sensitive values are present; an `.env` file is not required.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.
## Usage
Deploy the stack:
```bash
docker compose up -d
```
Access Quickchart:

The API is available at `http://localhost:8480`.
## Operational Notes
The Quickchart service is stateless. It does not require persistent storage for its core functionality as it generates chart images on demand.
## Known Limitations
This stack does not include mechanisms for custom fonts, themes, or other advanced Quickchart configurations that might require persistent storage or specific environment variables.
## Upstream Project
- Website: https://quickchart.io/
- GitHub: https://github.com/typpo/quickchart
## Final Notes
This stack provides a minimal, functional Quickchart instance. Adapt it to specific needs by adding a reverse proxy, SSL, and any required Quickchart-specific configuration.


