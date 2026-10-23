# Homepage

Personal home server dashboard.

## Access

- URL: http://<server-ip>:3000
- Project: `/srv/docker/homepage`
- Config: `/srv/docker/homepage/config`

## Files

- `compose.yaml`: Container configuration and pinned image version.
- `config/settings.yaml`: Theme and layout.
- `config/services.yaml`: Service links and availability checks.
- `config/widgets.yaml`: Resource monitoring and search.
- `config/bookmarks.yaml`: External links.

## Adding a service

Edit `config/services.yaml`, add a service under an existing or new category, then save. Homepage reloads configuration automatically.

Example:

```yaml
- Tools:
    - Example:
        href: http://<server-ip>:8080
        description: Example service
```

## Notes

- The image version is pinned in `compose.yaml`. Change it deliberately when upgrading.
- No Docker socket or Docker integration is enabled.
- Keep the dashboard accessible only on your trusted LAN.
- Back up `compose.yaml` and `config/`.
