# Media Automation

Docker Compose project for automating movie/TV downloads, library imports, and subtitles.

## Services
- **Gluetun:** VPN gateway; supports Mullvad or another compatible VPN provider.
- **qBittorrent:** Download client.
- **Jackett:** Torrent indexer aggregator.
- **Radarr:** Movie management and automation.
- **Sonarr:** TV series management and automation.
- **Bazarr:** Subtitle management.

## Paths
- Project: `/srv/docker/media-automation`
- Downloads: `/srv/media/downloads/movies`
- Movie library: `/srv/media/movies`
- Service configs: `/srv/docker/media-automation/*_config`
- Secrets: `/srv/docker/media-automation/.env`

## Initial Setup

Create the required directories and assign ownership to the user running the containers. Replace `1000:1000` if your configured `PUID`/`PGID` differ.

```bash
sudo mkdir -p /srv/media/downloads/movies /srv/media/movies
sudo chown -R 1000:1000 /srv/media/downloads /srv/media/movies
sudo chmod -R 775 /srv/media/downloads /srv/media/movies
```

Configure `.env` with the required VPN credentials and `PUID`/`PGID`. Requirements depend on the chosen provider; see the [Gluetun documentation](https://github.com/qdm12/gluetun-wiki).

## Access
Use the server's hostname or IP address with these ports:
- qBittorrent: `8080`
- Radarr: `7878`
- Sonarr: `8989`
- Jackett: `9117`
- Bazarr: `6767`

## Application Configuration

- **qBittorrent:** Set the download location to `/downloads/movies`. Under *Settings → Advanced*, select the network interface matching the Compose VPN setup. Verify VPN connectivity before enabling automation.
- **Radarr/Sonarr:** Add qBittorrent as the download client using its reachable service name and port. Add Jackett indexers, then configure the appropriate movie/TV root folder.
- **Bazarr:** Connect to Radarr and Sonarr using their service URLs and API keys; configure subtitle languages.
- **Jellyfin:** Point its movie library to `/srv/media/movies` on the host, or the equivalent path mounted inside its container.

Container paths must be consistent across Radarr/Sonarr and qBittorrent for completed downloads to import correctly. Verify the actual Compose volume mappings before using these paths.

## Security
- qBittorrent shares Gluetun's network namespace. Verify VPN routing and kill-switch behavior before automated downloads.
- Do not expose Web UIs to the public internet.
- Keep `.env` private (`chmod 600`) and never commit secrets to Git.
- Do not delete or overwrite existing media files.