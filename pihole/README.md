# Pi-hole

A network-wide ad blocker and DNS sinkhole.

## Purpose

To provide a readily deployable Pi-hole instance using Docker Compose for network-level ad blocking and DNS management.

## A Note from Matt

This Pi-hole config has been modified to fit my DNS resolution setup:

- BIND instances on port 53 and they resolve to Pi-hole instances
- Pi-hole instances run on port 5300 andd they resolve to Quad9 (9.9.9.9)

If you want to run Pi-hole with a vanilla config, head over to the project's repo: [https://github.com/pi-hole/docker-pi-hole](https://github.com/pi-hole/docker-pi-hole)

## What This Stack Includes

- Pi-hole DNS server and web interface
- Persistent storage for Pi-hole configuration
- Persistent storage for custom `dnsmasq` configurations

## Configuration Overview

A `.env` file is used to manage sensitive values, specifically the Pi-hole web interface password (`PIHOLE_WEBPASSWORD`). Other settings, such as `TZ` for timezone, are managed inline within the `docker-compose.yml`.

The web UI is intended to be accessed via a reverse proxy; the service itself is expected to remain within a trusted network boundary.

## Usage

1.  Create a `.env` file in the same directory as your `docker-compose.yml` with the following content:
    ```
    PIHOLE_WEBPASSWORD=your_secure_password
    ```
    Replace `your_secure_password` with a strong, unique password.
2.  Deploy the stack:
    ```bash
    docker compose up -d
    ```
3.  Configure network clients to use the Docker host's IP address as their primary DNS server on port 53.
4.  Access the Pi-hole web interface in a browser at `http://your_docker_host_ip/admin`. Log in using the password defined in `PIHOLE_WEBPASSWORD`.

## Operational Notes

-   **DNS Configuration**: For network-wide ad blocking, configure your router or individual client devices to use the Docker host's IP address as their primary DNS server.
-   **Password Management**: If you need to change the web interface password after deployment, you can use `docker compose exec pihole pihole -a -p`.
-   **DHCP Server**: Pi-hole can optionally function as a DHCP server. Exercise caution when enabling this feature, as it can conflict with existing DHCP servers on your network.
-   **Timezone**: Ensure the `TZ` environment variable in the `docker-compose.yml` accurately reflects your local timezone for correct log timestamps and scheduler operations.

### Known Limitations

-   Pi-hole primarily blocks ads at the DNS level; it does not block all in-page ads (e.g., YouTube ads) that are served from the same domain as the content. Browser-based ad blockers may be more effective for these scenarios.
-   Aggressive blocklists can inadvertently block legitimate content or break website functionality. Review blocklist choices and use the Pi-hole query log to troubleshoot issues.

## Upstream Project

-   Website: [https://pi-hole.net/](https://pi-hole.net/)
-   GitHub (Docker): [https://github.com/pi-hole/docker-pi-hole](https://github.com/pi-hole/docker-pi-hole)
-   GitHub (Core): [https://github.com/pi-hole/pi-hole](https://github.com/pi-hole/pi-hole)

## Final Notes

This stack provides a robust foundation for network-level content filtering. Regular maintenance and updates are recommended to maintain effectiveness and security.

