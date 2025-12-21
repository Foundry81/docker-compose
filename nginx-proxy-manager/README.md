# NGINX Proxy Manager
A web-based interface for managing NGINX reverse proxies with free SSL certificates.
## Purpose
Provides a self-contained, easy-to-deploy instance of NGINX Proxy Manager for routing external traffic to internal services and managing SSL certificates.
## What This Stack Includes
- One `nginx-proxy-manager` service.
- Persistent volumes for application data and Let's Encrypt certificates.
## Configuration Overview
Configuration is entirely inline within the `docker-compose.yml` file. No `.env` file is necessary as no sensitive values are present.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.
## Usage
To deploy the stack:
```bash
docker compose up -d
```
The NGINX Proxy Manager web interface is available on port `81`. NGINX services will be exposed on ports `80` and `443`.
## Operational Notes
This stack provides a simplified approach to managing NGINX reverse proxies and automating Let's Encrypt certificate issuance. All proxy hosts and SSL certificate configurations are managed through the web interface and persisted in the `data` and `letsencrypt` volumes.
## Known Limitations
While NGINX Proxy Manager simplifies common reverse proxy tasks, it may not support highly custom or complex NGINX configurations directly through its interface. Exposing the administration interface (port 81) directly to untrusted networks is discouraged.
## Upstream Project
- Website: [https://nginxproxymanager.com](https://nginxproxymanager.com)
- GitHub: [https://github.com/NginxProxyManager/nginx-proxy-manager](https://github.com/NginxProxyManager/nginx-proxy-manager)
## Final Notes
This stack offers a robust solution for centralizing proxy management and SSL termination.

