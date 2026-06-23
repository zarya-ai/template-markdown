# Dotfiles Organization Guide

**Purpose:** Organize and manage dotfiles across home lab, servers, and development environments

**Last Updated:** [FILL]

## Dotfiles Structure

```
dotfiles/
├── README.md
├── install.sh              # Installation script
├── .gitignore
├── .gitattributes
│
├── shell/                  # Shell configurations
│   ├── .bashrc
│   ├── .bash_profile
│   ├── .zshrc
│   ├── .zsh_profile
│   ├── .profile
│   └── aliases/            # Shell aliases
│       ├── common.sh
│       ├── dev.sh
│       └── docker.sh
│
├── editors/                # Editor configurations
│   ├── vim/
│   │   ├── .vimrc
│   │   └── .vim/
│   ├── neovim/
│   │   ├── init.vim
│   │   └── nvim/
│   └── vscode/
│       └── settings.json
│
├── git/                    # Git configurations
│   ├── .gitconfig
│   ├── .gitignore_global
│   └── hooks/              # Custom git hooks
│       ├── pre-commit
│       └── post-merge
│
├── ssh/                    # SSH configurations
│   ├── config
│   └── .ssh_template       # Template for keys (DO NOT COMMIT REAL KEYS)
│
├── dev/                    # Development tool configs
│   ├── .docker/
│   ├── .eslintrc
│   ├── .prettierrc
│   └── .editorconfig
│
├── system/                 # System configurations
│   ├── systemd/            # Systemd service files
│   │   └── *.service
│   ├── cron/               # Cron jobs
│   │   └── crontab.txt
│   └── network/            # Network configs
│       └── [FILL]
│
├── scripts/                # Utility scripts
│   ├── install.sh
│   ├── sync.sh
│   ├── backup.sh
│   └── setup-[FILL].sh
│
└── local/                  # Machine-specific (git ignored)
    ├── .bashrc.local
    ├── .gitconfig.local
    └── .env.local
```

## Installation Script

```bash
#!/bin/bash
# Dotfiles installation and linking script

set -euo pipefail

SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
BACKUP_DIR="${HOME}/.dotfiles.backup.$(date +%s)"

echo "Installing dotfiles from $SCRIPT_DIR"

# Create backup of existing dotfiles
if [[ -f "${HOME}/.bashrc" ]]; then
    mkdir -p "$BACKUP_DIR"
    cp "${HOME}/.bashrc" "$BACKUP_DIR/"
    echo "Backed up existing dotfiles to $BACKUP_DIR"
fi

# Create symlinks
echo "Creating symlinks..."

# Shell configs
ln -sf "${SCRIPT_DIR}/shell/.bashrc" "${HOME}/.bashrc"
ln -sf "${SCRIPT_DIR}/shell/.zshrc" "${HOME}/.zshrc"

# Git configs
ln -sf "${SCRIPT_DIR}/git/.gitconfig" "${HOME}/.gitconfig"
ln -sf "${SCRIPT_DIR}/git/.gitignore_global" "${HOME}/.gitignore_global"

# SSH config
ln -sf "${SCRIPT_DIR}/ssh/config" "${HOME}/.ssh/config"
chmod 600 "${HOME}/.ssh/config"

# [FILL — Additional symlinks]

echo "Dotfiles installed successfully!"
echo "Backup available at: $BACKUP_DIR"
```

## Best Practices

### Security

- **NEVER commit private keys or sensitive data**
- Use `.gitignore` to exclude:
  ```
  local/
  .ssh/
  *.local
  .env*
  *.key
  *.pem
  ```

- Use `.gitattributes` for file permissions:
  ```
  ssh/config diff=exif
  *.key diff=exif
  ```

### Organization

- Group related configs by category
- Use descriptive directory names
- Keep scripts in `scripts/` directory
- Use `local/` for machine-specific overrides

### Version Control

- Use semantic versioning (v1.0.0)
- Tag stable versions
- Document breaking changes in CHANGELOG
- Use branches for major refactoring

### Synchronization

**Sync to a new machine:**
```bash
git clone <repository> ~/.dotfiles
cd ~/.dotfiles
./scripts/install.sh
```

**Pull updates:**
```bash
cd ~/.dotfiles
git pull
./scripts/install.sh
```

**Push changes:**
```bash
cd ~/.dotfiles
git add .
git commit -m "Update [config]: [description]"
git push
```

## Machine-Specific Configuration

Use local files to override defaults:

**~/.bashrc**
```bash
# Load dotfiles bashrc
if [[ -f ~/.dotfiles/shell/.bashrc ]]; then
    source ~/.dotfiles/shell/.bashrc
fi

# Load local overrides
if [[ -f ~/.bashrc.local ]]; then
    source ~/.bashrc.local
fi
```

**~/.gitconfig**
```ini
[include]
    path = ~/.dotfiles/git/.gitconfig

[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig.local
```

## Common Patterns

### Conditional Loading by Environment

```bash
# In shell config
if [[ "$OSTYPE" == "linux-gnu"* ]]; then
    source ~/.dotfiles/shell/aliases/linux.sh
elif [[ "$OSTYPE" == "darwin"* ]]; then
    source ~/.dotfiles/shell/aliases/macos.sh
fi
```

### Function Organization

```bash
# shell/functions/common.sh
function project_cd() {
    cd ~/projects/"$1" || exit
}

# shell/.bashrc
source ~/.dotfiles/shell/functions/common.sh
```

### Alias Management

```bash
# shell/aliases/docker.sh
alias dc='docker-compose'
alias dcu='docker-compose up -d'
alias dcd='docker-compose down'

# shell/.bashrc
if command -v docker &> /dev/null; then
    source ~/.dotfiles/shell/aliases/docker.sh
fi
```

## Maintenance

**Regular review:**
- [ ] Remove unused configs
- [ ] Update comments
- [ ] Test on clean install
- [ ] Check for security issues

**Documentation:**
- Keep README updated
- Document what each file does
- Provide installation instructions
- List dependencies

## Notes

[FILL]
