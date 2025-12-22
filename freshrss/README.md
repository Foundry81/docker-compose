# FreshRSS
RSS feed aggregator.

## Purpose
This stack provides a self-hosted FreshRSS instance.
## What This Stack Includes
- FreshRSS service (`freshrss/freshrss:edge`)
- Persistent volume for FreshRSS application data (`./data`)
- Persistent volume for FreshRSS extensions (`./extensions`)
 
### Configuration Overview
This stack uses inline configuration within `docker-compose.yml`. No sensitive values are present, so a dedicated `.env` file is not required.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
Deploy the stack:
```bash
docker compose up -d
```
Access the FreshRSS web UI at `http://localhost:8400` or via your configured reverse proxy. Complete the initial setup through the web interface.

## Operational Notes
- The `CRON_MIN` environment variable configures the update frequency. Adjust this as needed for your feed update requirements.
- If using a reverse proxy, uncomment and configure the `TRUSTED_PROXY` environment variable with the IP address or CIDR of your proxy.

## Known Limitations
None.

## Upstream Project
- Website: <https://freshrss.org/>
- GitHub: <https://github.com/FreshRSS/FreshRSS>

## Final Notes\n\nThis stack provides a minimal, self-contained FreshRSS deployment. Adapt to your environment as necessary.

