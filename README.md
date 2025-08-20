# Tekkit Classic Docker Server

A containerized Tekkit Classic Minecraft server.

## Quick Start

```bash
git clone <your-repo-url>
cd tekkit-classic-docker
docker compose up -d
```

That's it! Your server will be available at `localhost:25565`.

## View Logs

```bash
docker compose logs -f
```

## Configuration (Optional)

Create a `.env` file to customize settings:

```bash
cp .env.example .env
# Edit .env with your preferred settings
docker compose up -d
```

### Common Settings

| Variable | Default | Description |
|----------|---------|-------------|
| `JAVA_MEMORY` | `2G` | Java heap size |
| `SERVER_PORT` | `25565` | Server port |
| `MAX_PLAYERS` | `20` | Maximum players |
| `MOTD` | `Tekkit Classic Server` | Server description |
| `DIFFICULTY` | `1` | 0=Peaceful, 1=Easy, 2=Normal, 3=Hard |

## Management

### Restart Server
```bash
docker compose restart
```

### Stop Server
```bash
docker compose down
```

### Access Console
```bash
docker compose exec tekkit mc-console
```

### Give Op Permissions
```bash
docker compose exec tekkit mc-op <username>
```

### Create Backup
```bash
docker compose exec tekkit tar -czf /tmp/backup.tar.gz -C /server world
docker compose cp tekkit:/tmp/backup.tar.gz ./backup-$(date +%Y%m%d).tar.gz
```

### Restore Backup
```bash
docker compose down
docker compose cp ./backup-20240101.tar.gz tekkit:/tmp/restore.tar.gz
docker compose up -d
docker compose exec tekkit tar -xzf /tmp/restore.tar.gz -C /server
docker compose restart
```

## Data Persistence

All server data is automatically saved in a Docker volume:
- All server files: `tekkit-server-data`

This includes worlds, configuration files, mods, and logs.

To completely remove all data:
```bash
docker compose down -v
```

## Troubleshooting

### Permission Issues
If you see permission denied errors:
```bash
sudo chown -R 1000:1000 ./server-data
```

### Check Server Status
```bash
docker compose ps
docker compose exec tekkit mc-health
```

### Memory Issues
Increase memory allocation in `.env`:
```env
JAVA_MEMORY=4G
```

## License

MIT License