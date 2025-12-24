# Chrony

This stack deploys a Chrony Network Time Protocol (NTP) server.

## Purpose

Provides a local NTP server for synchronized timekeeping within a Docker environment or for clients on the host network.

## What This Stack Includes

-   `ntp` service running the `simonrupf/chronyd:latest` image.
-   Exposes UDP port 123 for NTP client access.
-   Utilizes `tmpfs` mounts for volatile runtime data directories (`/etc/chrony`, `/run/chrony`, `/var/lib/chrony`).
-   Adds `CAP_NET_BIND_SERVICE` and `SYS_TIME` capabilities for binding privileged ports and adjusting system time.
-   Mounts `/dev/ptp0` for Precision Time Protocol (PTP) hardware support.

## Configuration Overview

All configuration is managed via environment variables directly within the `docker-compose.yml` file. No `.env` file is necessary as no sensitive values are present.

## Usage

Deploy the stack:

```bash
docker compose up -d
```

Access the NTP server by pointing clients to the host's IP address on UDP port 123. For example, using `ntpdate` or configuring `chrony` or `ntpd` clients:

```bash
ntpdate -u <HOST_IP>
```

## Operational Notes

-   The service is configured with `read_only: true` and `tmpfs` mounts for `/etc/chrony`, `/run/chrony`, and `/var/lib/chrony`, ensuring a clean state on restart and minimizing disk writes.
-   `CAP_NET_BIND_SERVICE` allows the container to bind to port 123. `SYS_TIME` permits adjusting the system clock within the container, which is critical for an NTP daemon.
-   The `TZ` environment variable is set to `America/Mew_York`, which appears to be a typo. Correct it to a valid timezone name (e.g., `America/New_York`) for accurate local time reporting.
-   `NTP_SERVERS` is configured to use `time.cloudflare.com` as the upstream source. Adjust this as required.

## Known Limitations

-   The `/dev/ptp0` device mount requires a host system with PTP hardware support and the corresponding kernel modules. If unavailable, the mount may fail or the container might not leverage PTP functionality.
-   Running this stack requires UDP port 123 to be free on the host. It may conflict with an existing NTP daemon on the host system.

## Upstream Project

-   Website: <https://chrony.tuxfamily.org/>
-   GitHub: <https://github.com/mlichvar/chrony>

## Final Notes

This Chrony stack provides a robust time synchronization solution. Ensure host-level time services do not conflict.
