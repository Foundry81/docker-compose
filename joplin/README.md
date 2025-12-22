# Joplin Server
Joplin Server provides a backend for syncing Joplin clients and includes an optional AI-powered transcription service.

## Purpose
This stack provides a complete, self-hosted deployment of Joplin Server with its required PostgreSQL database. It includes the optional Joplin Transcribe service for AI-powered audio transcription.

## What This Stack Includes
- **db**: PostgreSQL database for Joplin Server.
- **app**: Joplin Server application.
- **transcribe-db**: PostgreSQL database for the Transcribe service.
- **transcribe**: Joplin Transcribe service, offering AI audio transcription.

### Configuration Overview
This stack uses a `.env` file for managing sensitive credentials and deployment-specific settings such as database passwords, API keys, and the application's base URL. Copy the provided `.env.example` to `.env` and adjust values as required.
The `app` service exposes a web UI. The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage
Create a `.env` file from the provided `.env.example` and populate the variables:
```bash
cp .env.example .env\n    # Edit .env to set your secrets and configuration
```
Start the stack using Docker Compose.
To run Joplin Server only (without the Transcribe service):
```bash
docker compose --profile server up -d
```
To run Joplin Server with the Transcribe service:
```bash
docker compose --profile full up -d
```
Access Joplin Server via the `APP_BASE_URL` configured in your `.env` file.

## Docker Socket Notes
The `transcribe` service mounts `/var/run/docker.sock`. This grants the container elevated access to the host's Docker daemon. Exercise caution and ensure you fully trust the container image and its configuration before deploying.

## Operational Notes
- Ensure `APP_BASE_URL` in your `.env` file accurately reflects the public URL where Joplin Server will be accessible. This is critical for client synchronization.
- The `transcribe` service is optional. Use `--profile server` to exclude it or `--profile full` to include it.
- The `transcribe` service requires the host path specified by `HTR_CLI_IMAGES_FOLDER` to be mounted for image storage. Ensure this path exists and has correct permissions on your host.\n\n

### Known Limitations
- The `transcribe` service requires host Docker socket access, which introduces a security risk.

## Upstream Project
- Website: [Joplin](https://joplinapp.org/)
- GitHub: [laurent22/joplin](https://github.com/laurent22/joplin)
- ## Final Notes
- Prioritize securing Joplin Server with TLS via a reverse proxy for any deployment exposed beyond a trusted network.

