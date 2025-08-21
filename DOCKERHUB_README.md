# Tekkit Classic Docker Server

A containerized Tekkit Classic Minecraft server with sensible defaults and easy configuration. Automatically built from source with support for both x86_64 and ARM64 architectures.

## Quick Start

**Simple Setup:**
```bash
docker run -d \
  -p 25565:25565 \
  -v tekkit-data:/server \
  --name tekkit-server \
  wizardnun/tekkit-classic
```

**With Docker Compose:**

Create a `docker-compose.yml` file:
```yaml
services:
  tekkit:
    image: wizardnun/tekkit-classic
    container_name: tekkit-classic
    restart: unless-stopped
    ports:
      - "25565:25565"
    volumes:
      - tekkit-server-data:/server
    environment:
      - JAVA_MEMORY=4G
      - MAX_PLAYERS=20
      - ONLINE_MODE=false

volumes:
  tekkit-server-data:
```

Then run: `docker compose up -d`

Your server will be available at `localhost:25565`.

## Configuration

Configure the server using environment variables:

| Variable | Default | Description |
|----------|---------|-------------|
| `JAVA_MEMORY` | `4G` | Java heap size (1G, 2G, 4G, 8G) |
| `SERVER_PORT` | `25565` | Server port |
| `MAX_PLAYERS` | `20` | Maximum players |
| `MOTD` | `Tekkit Classic Server` | Server description |
| `DIFFICULTY` | `1` | 0=Peaceful, 1=Easy, 2=Normal, 3=Hard |
| `PVP` | `true` | Enable PVP |
| `ALLOW_FLIGHT` | `true` | Allow flight |
| `VIEW_DISTANCE` | `10` | View distance in chunks |
| `ONLINE_MODE` | `false` | Verify Minecraft accounts |

### Example with Custom Settings

```bash
docker run -d \
  -p 25565:25565 \
  -e JAVA_MEMORY=4G \
  -e MAX_PLAYERS=50 \
  -e MOTD="My Awesome Tekkit Server" \
  -e DIFFICULTY=2 \
  -e ONLINE_MODE=false \
  -v tekkit-data:/server \
  --name tekkit-server \
  wizardnun/tekkit-classic
```

## Management

### View Logs
```bash
docker logs -f tekkit-server
```

### Access Console
```bash
docker exec -it tekkit-server mc-console
```

### Give Op Permissions
```bash
docker exec tekkit-server mc-op <username>
```

### Health Check
```bash
docker exec tekkit-server mc-health
```

### Restart Server
```bash
docker restart tekkit-server
```

### Stop and Remove
```bash
docker stop tekkit-server
docker rm tekkit-server
```

## Port Requirements

- **25565/tcp** - Minecraft server (required)

Make sure this port is not blocked by firewall and is properly forwarded if running on a remote server.

## System Requirements

- **Minimum:** 2GB RAM, 2 CPU cores, 5GB disk space
- **Recommended:** 4GB+ RAM, 4+ CPU cores, 10GB+ disk space
- **OS:** Any system with Docker support (Linux, macOS, Windows)

## Source Code

Full source code, development documentation, and issue tracking available at:
[GitHub Repository](https://github.com/jiffy953/Tekkit-Classic-Docker)

## Images

- **Latest:** `wizardnun/tekkit-classic:latest`
- **Versioned:** `wizardnun/tekkit-classic:v1.0`

Images are automatically built from source using GitHub Actions and support both AMD64 and ARM64 architectures.

## License

MIT License