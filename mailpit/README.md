# Mailpit
Mailpit is a lightweight SMTP testing service used to safely capture, inspect, and debug outbound email without delivering it to real inboxes.

## Purpose
This stack exists to support application development and lab environments where email needs to be observed, not trusted.

The web UI is intended to be accessed via a reverse proxy; SMTP is expected to remain within a trusted network boundary.

Mailpit is used here as a drop-in SMTP sink:

- Applications send mail normally
- Messages are captured locally
- Nothing leaves the environment

This replaces older tools like MailHog with a faster, actively maintained alternative.

## What This Stack Includes

- Mailpit SMTP service
- Mailpit web UI for inspecting captured messages
- Persistent storage for retained mail
- Single service. Minimal moving parts. No supporting containers required.

## Configuration Overview

This stack is intentionally configured inline in the Compose file.

No .env file is used because:

- There are no secrets
- The configuration surface is small
- The values benefit from being visible

Current configuration:

- SMTP exposed on port 25 (mapped to Mailpit’s internal 1025)
- Web UI exposed on port 8025
- Message retention capped at 5,000 messages
- Mail persisted to a local SQLite database
- SMTP authentication accepted but not enforced (testing only)

If you change ports or retention behavior, do it directly in the Compose file.

The web UI is intended to be accessed via a reverse proxy; SMTP is expected to remain within a trusted network boundary.

## Usage
Start the service:
`docker compose up -d`

Then:
- Point applications at the host’s SMTP port 25
- Open http://<host>:8025 to view captured messages

No email is delivered externally.

Operational Notes
- This configuration is not suitable for real mail delivery
- SMTP auth is permissive by design - do not expose this service publicly
- Captured emails may contain credentials, tokens, or reset links
- Persistent storage will grow over time if messages are not pruned

Treat this service as disposable infrastructure with sensitive visibility.

## Known Limitations
- No outbound mail delivery
- No mail routing or filtering
- No security hardening beyond “don’t expose it”

If you need a real MTA, this is the wrong tool on purpose.

## Upstream Project
- Website: https://mailpit.axllent.org
- GitHub: https://github.com/axllent/mailpit

All credit belongs upstream. This stack exists to make local integration easy.

## Final Notes

This Compose file reflects a testing-first mindset:
- Visibility over security
- Convenience over correctness
- Speed over ceremony

If your application sends email and you’re not inspecting it during development, you’re debugging blind.

