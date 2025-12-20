# Dillinger
Dillinger is a straightforward, self-hosted Markdown editor. It’s simple, fast, and does what it promises without extra ceremony.

## Purpose
This stack exists to provide a lightweight, browser-based Markdown editor for personal or lab use.

Dillinger is used here as:
- A quick internal tool for note-taking or documentation
- A low-friction alternative to desktop editors
- A clean, no-nonsense interface for Markdown

**Note:** Dillinger is in maintenance mode, so no major feature updates are expected. It’s stable, reliable, and sufficient for everyday use.

## What This Stack Includes
- Dillinger web application
- Persistent storage (browser storage) for user preferences and session data
- Single container, minimal configuration, no unnecessary dependencies.

## Configuration Overview
This stack is intentionally configured inline in the Compose file. No .env is needed.

Current configuration highlights:
- Container runs as user ID 1000 and group ID 1000 for local file permissions
- Timezone set to America/New_York
- Configuration persisted to ./config on the host
- Web UI exposed on port 8008 (mapped from container port 8080)

## Usage
Start the service:
```
docker compose up -d
```
### Then:
Access the UI at `http://<host>:8008`

Start editing Markdown immediately

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

### Operational Notes

- Dillinger stores user configuration and session data in ./config
- No authentication is included by default
- No multi-user features; treat as a personal tool or trusted lab service
- Simple, stable, low-maintenance deployment

## Known Limitations
- In maintenance mode: no new features expected
- No user management or role-based access
- Not designed for internet-facing deployments without additional security
- Limited to Markdown editing only

## Upstream Project
- GitHub: https://github.com/joemccann/dillinger
- Credit goes upstream. This stack exists to make self-hosting quick and painless.

## Final Notes
Dillinger works best as an internal tool for Markdown editing:
- Simple
- Low fuss
- Reliable

If you need a modern, multi-user editor with active development, this may not be the right choice. 
For fast, internal Markdown work, it’s perfect.

