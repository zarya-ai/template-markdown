# Dockerfile Template

**Application Name:** [FILL]

**Base Image:** [FILL]

**Version:** [FILL]

**Last Updated:** [FILL]

## Dockerfile

```dockerfile
# [FILL — Stage 1: Builder/Base]
FROM [FILL — base-image:tag] AS builder

# Metadata
LABEL maintainer="[FILL]"
LABEL description="[FILL — Description of container]"
LABEL version="[FILL]"

# Set working directory
WORKDIR /app

# [FILL — Install build dependencies]
RUN apt-get update && apt-get install -y --no-install-recommends \
    [FILL] \
    [FILL] \
    && rm -rf /var/lib/apt/lists/*

# Copy source files
COPY . .

# [FILL — Build steps]
RUN [FILL]

---

# [FILL — Stage 2: Runtime]
FROM [FILL — runtime-image:tag]

# Metadata
LABEL maintainer="[FILL]"
LABEL description="[FILL]"

# Set working directory
WORKDIR /app

# Create non-root user
RUN groupadd -r appuser && useradd -r -g appuser appuser

# [FILL — Install runtime dependencies]
RUN apt-get update && apt-get install -y --no-install-recommends \
    [FILL] \
    && rm -rf /var/lib/apt/lists/*

# Copy artifacts from builder
COPY --from=builder /app . \
    --chown=appuser:appuser

# [FILL — Copy configuration files]
COPY --chown=appuser:appuser config/ ./config/

# [FILL — Environment variables]
ENV [FILL]=value
ENV [FILL]=value

# Expose ports
EXPOSE [FILL]/tcp [FILL]/tcp

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD [FILL — health check command]

# Switch to non-root user
USER appuser

# Set entrypoint
ENTRYPOINT ["/app/entrypoint.sh"]

# Set default command
CMD ["/app/start.sh"]
```

## Best Practices Applied

- [x] Multi-stage build for smaller image size
- [x] Non-root user for security
- [x] Minimal base image
- [x] Layer caching optimization
- [x] Health checks configured
- [x] Clear metadata labels
- [x] Dependency pinning
- [x] Apt cache cleanup

## Build Instructions

**Build command:**
```bash
docker build -t [FILL]:latest .
```

**Build with arguments:**
```bash
docker build --build-arg [FILL]=value -t [FILL]:latest .
```

## Run Instructions

**Basic run:**
```bash
docker run -d \
  --name [FILL] \
  -p [FILL]:[FILL] \
  [FILL]:latest
```

**With environment variables:**
```bash
docker run -d \
  --name [FILL] \
  -e [FILL]=value \
  -p [FILL]:[FILL] \
  [FILL]:latest
```

**With volume mounts:**
```bash
docker run -d \
  --name [FILL] \
  -v /host/path:/container/path \
  -p [FILL]:[FILL] \
  [FILL]:latest
```

## Notes

[FILL]
