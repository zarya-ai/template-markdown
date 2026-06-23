# Development Environment Setup

**Environment Name:** [FILL]

**Purpose:** [FILL]

**Last Updated:** [FILL]

## Setup Script

```bash
#!/bin/bash

################################################################################
# Development Environment Setup
################################################################################
# Purpose: Initialize development environment with all required tools
# Author: [FILL]
# Version: [FILL]

set -euo pipefail

SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

# Color output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m'

log_info() { echo -e "${GREEN}[INFO]${NC} $*"; }
log_warn() { echo -e "${YELLOW}[WARN]${NC} $*" >&2; }
log_error() { echo -e "${RED}[ERROR]${NC} $*" >&2; }

################################################################################
# System Dependencies
################################################################################

install_system_deps() {
    log_info "Installing system dependencies..."
    
    if [[ -f /etc/os-release ]]; then
        . /etc/os-release
        
        case "$ID" in
            ubuntu|debian)
                sudo apt-get update
                sudo apt-get install -y \
                    build-essential \
                    curl \
                    git \
                    wget \
                    [FILL]
                ;;
            centos|rhel|fedora)
                sudo yum install -y \
                    gcc \
                    curl \
                    git \
                    wget \
                    [FILL]
                ;;
            *)
                log_warn "Unsupported OS: $ID"
                ;;
        esac
    fi
}

################################################################################
# Language Runtimes
################################################################################

install_python() {
    log_info "Installing Python..."
    
    if ! command -v python3 &> /dev/null; then
        sudo apt-get install -y python3 python3-pip python3-venv
    fi
    
    python3 --version
}

install_nodejs() {
    log_info "Installing Node.js..."
    
    if ! command -v node &> /dev/null; then
        curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
        sudo apt-get install -y nodejs
    fi
    
    node --version
    npm --version
}

install_docker() {
    log_info "Installing Docker..."
    
    if ! command -v docker &> /dev/null; then
        curl -fsSL https://get.docker.com -o get-docker.sh
        sudo sh get-docker.sh
        sudo usermod -aG docker "$USER"
        rm get-docker.sh
    fi
    
    docker --version
}

################################################################################
# Development Tools
################################################################################

install_dev_tools() {
    log_info "Installing development tools..."
    
    # Git configuration
    git config --global user.name "[FILL]"
    git config --global user.email "[FILL]"
    git config --global core.editor vim
    
    # [FILL — Additional tool installations]
}

################################################################################
# Project Setup
################################################################################

setup_project() {
    log_info "Setting up project..."
    
    # Python virtual environment
    if [[ -f requirements.txt ]]; then
        python3 -m venv venv
        source venv/bin/activate
        pip install --upgrade pip
        pip install -r requirements.txt
    fi
    
    # Node.js dependencies
    if [[ -f package.json ]]; then
        npm install
    fi
    
    # [FILL — Additional setup]
}

################################################################################
# Verification
################################################################################

verify_setup() {
    log_info "Verifying setup..."
    
    local errors=0
    
    # Check required commands
    local required_cmds=("git" "curl" "docker" "python3" "node")
    for cmd in "${required_cmds[@]}"; do
        if ! command -v "$cmd" &> /dev/null; then
            log_error "Missing required command: $cmd"
            ((errors++))
        fi
    done
    
    if [[ $errors -eq 0 ]]; then
        log_info "Setup verification passed!"
        return 0
    else
        log_error "Setup verification failed with $errors errors"
        return 1
    fi
}

################################################################################
# Main
################################################################################

main() {
    log_info "Starting development environment setup..."
    
    install_system_deps
    install_python
    install_nodejs
    install_docker
    install_dev_tools
    setup_project
    verify_setup
    
    log_info "Setup completed successfully!"
}

main "$@"
```

## Requirements

**System:**
- [FILL] OS
- [FILL] GB RAM
- [FILL] GB disk space

**Required tools:**
- [FILL]
- [FILL]
- [FILL]

## Installation Steps

1. **Clone repository:**
   ```bash
   git clone [FILL]
   cd [FILL]
   ```

2. **Run setup script:**
   ```bash
   ./scripts/setup.sh
   ```

3. **Activate virtual environment (Python):**
   ```bash
   source venv/bin/activate
   ```

4. **Start development:**
   ```bash
   make dev
   ```

## Environment Variables

**Create `.env` file:**
```bash
cp .env.example .env
# Edit .env with your values
```

**Required variables:**
- `[FILL]` — [Description]
- `[FILL]` — [Description]

## Troubleshooting

**Permission denied errors:**
```bash
sudo chown -R "$USER" .
```

**Docker permission issues:**
```bash
sudo usermod -aG docker "$USER"
newgrp docker
```

**Python venv not working:**
```bash
rm -rf venv
python3 -m venv venv
source venv/bin/activate
```

## Notes

[FILL]
