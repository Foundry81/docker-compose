# HomeAssistant

A powerful open-source home automation platform.

## Purpose

This stack provides a straightforward method to deploy Home Assistant within a Docker environment, ensuring application and configuration persistence.

## What This Stack Includes

-   The Home Assistant application service.
-   A persistent configuration directory mounted from `./config`.
-   Read-only access to the host's `localtime` for correct time synchronization.
-   Read-only access to the host's D-Bus socket (`/run/dbus`).
-   Direct access to a specified serial device (`/dev/ttyACM0`).

### Configuration Overview

All configuration is handled either through mounted volumes or inline within the `docker-compose.yml` file. A dedicated `.env` file is not justified as there are no sensitive or frequently changing environment variables required by this stack.

The Home Assistant service runs in `host` network mode, directly exposing its default port (8123) on the host's network interfaces. The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

To deploy this stack:

```bash
docker compose up -d
```

Access the Home Assistant web interface at `http://<your-host-ip>:8123`.

## Operational Notes

-   **Host Network Mode**: This stack utilizes `network_mode: host`. This configuration grants Home Assistant direct access to the host's network interfaces and ports. Be aware of potential port conflicts if other services on the host use port 8123.
-   **Serial Device Access**: The stack is configured to pass `/dev/ttyACM0` into the container. Adjust this path in `docker-compose.yml` if your serial device (e.g., Z-Wave, Zigbee dongle) is located elsewhere or requires a different device file.
-   **D-Bus Access**: Read-only access to `/run/dbus` is provided. This may be required for certain advanced integrations or hardware interactions.
-   **Privileged Mode**: The Home Assistant container does not run in `privileged` mode, enhancing security posture.

### Known Limitations

-   Using `network_mode: host` reduces container isolation and can lead to port conflicts on the host system.
-   The specified serial device path (`/dev/ttyACM0`) must exist on the host and correspond to the intended hardware.

## Upstream Project

-   Website: https://www.home-assistant.io/
-   GitHub: https://github.com/home-assistant/core

## Final Notes

Home Assistant offers extensive flexibility for smart home integration. Plan your integrations carefully to optimize performance and resource usage.

