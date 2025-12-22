# IT-Tools
A collection of web-based tools for developers and IT professionals.

## Purpose
This stack provides a self-hosted instance of IT-Tools, offering a convenient suite of utilities for development and system administration tasks.

## What This Stack Includes
- One `it-tools` service based on `corentinth/it-tools:latest`.
- A persistent container restart policy.
- Host port `8780` mapped to container port `8080` for web access.

## Configuration Overview
All configuration is inline within the `compose.yml` file. No `.env` file is necessary as there are no sensitive or frequently changed variables.
The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
Deploy the stack:
```bash
docker compose up -d
```
Access the web UI at `http://localhost:8780` or via your configured reverse proxy.

## Operational Notes
IT-Tools offers a quick, local alternative to various online converters, formatters, and generators, useful for everyday development and troubleshooting

## Known Limitations\n\nThis stack provides the base IT-Tools application without any advanced features or integrations.

## Upstream Project
- GitHub: https://github.com/CorentinTh/it-tools

## Final Notes
This stack delivers a functional, minimal deployment of IT-Tools.

