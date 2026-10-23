# Home Server

A self-hosted home server managed with Docker Compose. This repository contains service definitions and configuration for running the setup on your own machine.

## Services

- **Beszel:** Server monitoring
- **Homepage:** Home dashboard
- **Immich:** Photo and video management
- **Jellyfin:** Media streaming
- **Media Automation:** Download and media library management using Gluetun, qBittorrent, Radarr, Sonarr, Jackett, and Bazarr
- **Pi-hole:** Network-wide DNS filtering

## Requirements

- Linux server with Docker Engine and Docker Compose
- Sufficient storage for application data and media
- Service-specific configuration and credentials as documented in each directory

## Setup

1. Clone this repository.
2. Review the README in each service directory.
3. Create the required `.env` files from the corresponding `.env.example` files.
4. Configure your own paths, credentials, and server-specific values.
5. Start each service from its directory using Docker Compose.

## Repository Structure

```text
.
├── beszel/
├── homepage/
├── immich/
├── jellyfin/
├── media-automation/
└── pihole/
```

Each directory contains its Docker Compose definition and, where applicable, configuration examples and service-specific documentation.

## Security and Data

- Never commit `.env` files, passwords, API keys, private keys, or other secrets.
- Review configuration files before publishing changes.
- Persistent application data and databases are not managed by this repository. Back them up separately.
- Do not expose service dashboards directly to the public internet without appropriate security controls.
- Verify VPN connectivity before enabling automated downloads in the media automation stack.

## Customization

This repository is intended as a reusable starting point. Adjust host paths, environment variables, ports, and service settings for your environment before deployment.