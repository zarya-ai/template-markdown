# Docker Compose Template

**Project Name:** [FILL]

**Version:** [FILL]

**Last Updated:** [FILL]

## docker-compose.yml

```yaml
# [FILL — Project Description]
# Version: [FILL]
# Author: [FILL]

version: '3.9'

services:
  # [FILL — Service 1]
  [FILL]:
    image: [FILL]:latest
    container_name: [FILL]
    
    # Restart policy
    restart: unless-stopped
    
    # Environment variables
    environment:
      - [FILL]=value
      - [FILL]=value
    
    # Port mappings
    ports:
      - "[FILL]:[FILL]/tcp"
      - "[FILL]:[FILL]/tcp"
    
    # Volume mounts
    volumes:
      - [FILL]_data:/data
      - ./config:/app/config:ro
    
    # Networks
    networks:
      - [FILL]
    
    # Resource limits
    deploy:
      resources:
        limits:
          cpus: '[FILL]'
          memory: '[FILL]'
        reservations:
          cpus: '[FILL]'
          memory: '[FILL]'
    
    # Health check
    healthcheck:
      test: ["CMD", "[FILL]"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
    
    # Logging
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
    
    # Depends on
    depends_on:
      [FILL]:
        condition: service_healthy
  
  # [FILL — Service 2]
  [FILL]:
    image: [FILL]:latest
    container_name: [FILL]
    restart: unless-stopped
    environment:
      - [FILL]=value
    volumes:
      - [FILL]_data:/data
    networks:
      - [FILL]

volumes:
  [FILL]_data:
    driver: local
  [FILL]_data:
    driver: local

networks:
  [FILL]:
    driver: bridge
```

## Services

### [FILL — Service Name]

**Image:** [FILL]

**Purpose:** [FILL]

**Ports:** [FILL]

**Environment Variables:**
- `[FILL]` — [Description]
- `[FILL]` — [Description]

**Volumes:**
- `[FILL]` — [Description]

**Dependencies:** [FILL]

### [FILL — Service Name]

**Image:** [FILL]

**Purpose:** [FILL]

**Ports:** [FILL]

**Environment Variables:**
- `[FILL]` — [Description]

**Volumes:**
- `[FILL]` — [Description]

## Usage

**Start all services:**
```bash
docker-compose up -d
```

**Stop all services:**
```bash
docker-compose down
```

**View logs:**
```bash
docker-compose logs -f [service-name]
```

**Execute command in service:**
```bash
docker-compose exec [service-name] [command]
```

**Rebuild services:**
```bash
docker-compose up -d --build
```

## Configuration

**Environment files:**
- `.env` — Create from `.env.example`
- `.env.local` — Local overrides (git ignored)

**Required environment variables:**
- `[FILL]` — [Description]
- `[FILL]` — [Description]

## Network Configuration

**Network:** `[FILL]` (bridge)

**Service DNS names:**
- `[FILL]` — Service accessible at this hostname
- `[FILL]` — Service accessible at this hostname

## Volumes

**Persistent volumes:**
- `[FILL]_data` — [Description]
- `[FILL]_data` — [Description]

## Backup & Restore

**Backup volumes:**
```bash
docker-compose exec [service] tar czf /backup/backup.tar.gz /data
```

**Restore volumes:**
```bash
docker-compose exec [service] tar xzf /backup/backup.tar.gz -C /
```

## Monitoring

**Service health:**
```bash
docker-compose ps
```

**Resource usage:**
```bash
docker stats
```

## Notes

[FILL]
