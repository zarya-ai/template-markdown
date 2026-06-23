# Code Snippet Reference & Library

**Project:** [FILL]

**Purpose:** Centralized repository for frequently used code snippets and patterns

**Last Updated:** [FILL]

## Organization

```
snippets/
├── shell/                  # Bash/Shell snippets
│   ├── error-handling.sh
│   ├── file-operations.sh
│   └── system-admin.sh
├── python/                 # Python snippets
│   ├── decorators.py
│   ├── error-handling.py
│   └── data-processing.py
├── docker/                 # Docker snippets
│   ├── dockerfile-patterns.md
│   └── docker-compose-examples.md
├── yaml/                   # YAML configuration snippets
│   ├── kubernetes.yaml
│   └── docker-compose.yaml
└── patterns/               # Design patterns & best practices
    ├── error-handling.md
    ├── logging.md
    └── configuration.md
```

## Shell Snippets

### Error Handling Pattern

```bash
set -euo pipefail

error_exit() {
    echo "Error: $1" >&2
    exit "${2:-1}"
}

# Usage
command || error_exit "Command failed"
```

### Logging Functions

```bash
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m'

log_info() { echo -e "${GREEN}[INFO]${NC} $*"; }
log_warn() { echo -e "${YELLOW}[WARN]${NC} $*" >&2; }
log_error() { echo -e "${RED}[ERROR]${NC} $*" >&2; }
```

### File Operations

```bash
# Check if file exists
if [[ -f "$FILE" ]]; then
    echo "File exists"
fi

# Check if directory exists
if [[ -d "$DIR" ]]; then
    echo "Directory exists"
fi

# Create temporary file
TEMP_FILE="$(mktemp)"
trap "rm -f $TEMP_FILE" EXIT
```

### Argument Parsing

```bash
while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            usage
            exit 0
            ;;
        -v|--verbose)
            VERBOSE=true
            shift
            ;;
        -f|--file)
            FILE="$2"
            shift 2
            ;;
        *)
            echo "Unknown option: $1"
            exit 1
            ;;
    esac
done
```

## Python Snippets

### Error Handling & Logging

```python
import logging

logger = logging.getLogger(__name__)
logger.setLevel(logging.DEBUG)

handler = logging.StreamHandler()
handler.setFormatter(logging.Formatter(
    '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
))
logger.addHandler(handler)
```

### Configuration Management

```python
import os
from pathlib import Path
from dotenv import load_dotenv

load_dotenv()

class Config:
    DEBUG = os.getenv('DEBUG', 'False').lower() == 'true'
    DATABASE_URL = os.getenv('DATABASE_URL')
    SECRET_KEY = os.getenv('SECRET_KEY')
```

### Exception Handling

```python
class CustomError(Exception):
    """Base exception for custom errors"""
    pass

try:
    # Code that might fail
    result = dangerous_operation()
except ValueError as e:
    logger.error(f"Invalid value: {e}")
except Exception as e:
    logger.exception(f"Unexpected error: {e}")
else:
    logger.info(f"Operation succeeded: {result}")
finally:
    cleanup()
```

### Decorators

```python
import functools
import time

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"{func.__name__} took {time.time() - start:.2f}s")
        return result
    return wrapper

def retry(max_attempts=3, delay=1):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
                    time.sleep(delay)
        return wrapper
    return decorator
```

## Docker Snippets

### Multi-stage Build

```dockerfile
FROM python:3.11 AS builder
WORKDIR /build
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

FROM python:3.11-slim
WORKDIR /app
COPY --from=builder /usr/local/lib /usr/local/lib
COPY app.py .
CMD ["python", "app.py"]
```

### Health Check

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1
```

### Non-root User

```dockerfile
RUN groupadd -r appuser && useradd -r -g appuser appuser
USER appuser
```

## YAML Snippets

### Docker Compose Service

```yaml
services:
  app:
    image: myapp:latest
    container_name: myapp
    restart: unless-stopped
    environment:
      - DEBUG=false
    ports:
      - "8000:8000"
    volumes:
      - app_data:/data
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 3s
      retries: 3
```

### Environment Configuration

```yaml
app:
  name: myapp
  version: 1.0.0
  
  server:
    host: 0.0.0.0
    port: 8000
    
  database:
    host: ${DB_HOST:localhost}
    port: ${DB_PORT:5432}
    username: ${DB_USER}
    password: ${DB_PASSWORD}
```

## Patterns & Best Practices

### Error Handling Strategy

1. **Validate input early**
2. **Use specific exceptions**
3. **Log with context**
4. **Fail gracefully**
5. **Provide recovery options**

### Logging Strategy

1. **Use appropriate log levels**
   - DEBUG: Detailed diagnostics
   - INFO: General information
   - WARNING: Warning messages
   - ERROR: Error messages
   - CRITICAL: Critical errors

2. **Include context**
   - Timestamp
   - Logger name
   - Log level
   - Message

3. **Redirect to appropriate destinations**
   - stdout for application logs
   - stderr for errors
   - Files for persistence

### Configuration Management

1. **Hierarchy of configuration sources**
   - Defaults
   - Config files
   - Environment variables
   - Command-line arguments

2. **Environment-specific configs**
   - development
   - staging
   - production

3. **Secrets management**
   - Never commit secrets
   - Use `.env` files (git ignored)
   - Use secret management tools in production

## Quick Reference

**For [FILL — specific use case], use this snippet:**

```[FILL]
[FILL]
```

**For [FILL — another use case], use this pattern:**

```[FILL]
[FILL]
```

## Notes

[FILL]
