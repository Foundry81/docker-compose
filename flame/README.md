# Flame
Flame is a lightweight, self-hosted dashboard for organizing and accessing internal services through a clean, customizable web interface.

## Purpose
This stack exists to provide a simple, centralized landing page for lab and internal services.

Flame is used here as:
- A visual index for self-hosted tools
- A low-friction alternative to browser bookmarks
- A single place to organize services that tend to multiply over time

It is not meant to be a public portal.

## What This Stack Includes

- Flame web application
- Persistent storage for configuration and icons
- Optional Docker integration via the Docker socket

Single container, minimal setup, quick payoff.

## Configuration Overview
This stack uses environment variables for configuration.
- See `.env.example` for required values
- No secrets are committed to the repository
- You are expected to supply your own credentials

### Required configuration:
- PASSWORD - used to protect access to the Flame UI

The password is intentionally externalized to avoid accidental reuse or exposure.
## Usage
### Initial setup:
```
cp .env.example .env
docker compose up -d
```
### Once running:
- Access the UI on port 5005
- Log in using the configured password
- Begin adding and organizing services

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Docker Integration Notes
This stack mounts the Docker socket:
```
/var/run/docker.sock:/var/run/docker.sock
```
This is optional, but required if you want Flame to:
- Discover running containers
- Auto-populate services
- Display container metadata

Mounting the Docker socket grants the container elevated access to the host.

Do not enable this unless you understand the implications and trust the container.


If you do not need Docker integration, remove the mount.

## Operational Notes
- Flame stores configuration and icons on disk
- UI access is protected only by a single password
- There is no native multi-user or role-based access model

This service assumes a trusted audience.
## Known Limitations
- No fine-grained authentication or authorization
- No native SSO support
- Not designed for internet-facing deployments

If you need a hardened or multi-tenant dashboard, this is the wrong tool.

## Icons
This stack uses icons sourced from Self-Hosted Icons

Credit goes to the project for providing a comprehensive set of service icons for dashboards like Flame.

## Upstream Project
- GitHub: https://github.com/pawelmalak/flame

All credit belongs upstream. This stack exists to make local deployment straightforward.

## Final Notes
Flame works best when treated as internal glue:
- Useful
- Disposable
- Easy to rebuild

If your dashboard requires enterprise-grade access control, you’ve already outgrown this category of tool.

