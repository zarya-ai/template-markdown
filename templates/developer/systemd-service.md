# Systemd Service File Template

**Service Name:** [FILL]

**Description:** [FILL]

**Version:** [FILL]

## Service File: /etc/systemd/system/[FILL].service

```ini
# [FILL — Service Description]
# Purpose: [FILL]
# Author: [FILL]
# Version: [FILL]

[Unit]
# Service metadata
Description=[FILL — Human-readable service description]
Documentation=[FILL — URL to documentation]
After=network.target [FILL — other services]

# Dependency management
Requires=[FILL — required service]
Wants=[FILL — optional service]
PartOf=[FILL — service group]

[Service]
# Service type
Type=simple  # Options: simple, exec, forking, oneshot, dbus, notify, idle

# User and group
User=[FILL]
Group=[FILL]

# Working directory
WorkingDirectory=[FILL]

# Start command
ExecStart=[FILL — full path to executable]

# Pre-start commands
ExecStartPre=[FILL]

# Stop commands
ExecStop=[FILL]
ExecStopPost=[FILL]

# Restart behavior
Restart=on-failure  # Options: no, always, on-success, on-failure, on-abnormal, on-abort, on-watchdog
RestartSec=5s
StartLimitInterval=60s
StartLimitBurst=3

# Process management
KillMode=process  # Options: control-group, process, mixed, none
KillSignal=SIGTERM
TimeoutStopSec=30s

# Resource limits
LimitNOFILE=65536
LimitNPROC=512

# Security
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=[FILL]

# Environment variables
Environment="[FILL]=value"
Environment="[FILL]=value"
EnvironmentFile=[FILL — path to .env file]

# Standard output/error
StandardOutput=journal
StandardError=journal
SyslogIdentifier=[FILL]

# Logging
User=nobody
Group=nogroup

[Install]
# Enabling/disabling
WantedBy=multi-user.target  # Options: graphical.target, multi-user.target, rescue.target
RequiredBy=[FILL]
Alias=[FILL]
```

## Installation

**Create the service file:**
```bash
sudo nano /etc/systemd/system/[FILL].service
# Paste the above content
```

**Reload systemd daemon:**
```bash
sudo systemctl daemon-reload
```

**Enable service (start on boot):**
```bash
sudo systemctl enable [FILL].service
```

**Start service:**
```bash
sudo systemctl start [FILL].service
```

## Management Commands

**Check service status:**
```bash
sudo systemctl status [FILL].service
```

**View service logs:**
```bash
sudo journalctl -u [FILL].service -f
```

**View logs since last boot:**
```bash
sudo journalctl -u [FILL].service -b
```

**Stop service:**
```bash
sudo systemctl stop [FILL].service
```

**Restart service:**
```bash
sudo systemctl restart [FILL].service
```

**Reload service (without stopping):**
```bash
sudo systemctl reload [FILL].service
```

**Disable service (prevent auto-start):**
```bash
sudo systemctl disable [FILL].service
```

## Troubleshooting

**Service fails to start:**
```bash
# Check service file syntax
sudo systemd-analyze verify /etc/systemd/system/[FILL].service

# View detailed error log
sudo journalctl -u [FILL].service -n 50
```

**Service crashes repeatedly:**
```bash
# Check restart limit
sudo systemctl status [FILL].service

# Increase StartLimitBurst if needed
```

**Permissions denied errors:**
```bash
# Check file permissions
ls -la /path/to/executable

# Adjust User/Group in service file
```

## Common Service Types

### Simple (Long-running daemon)
```ini
Type=simple
ExecStart=/usr/bin/myapp --config=/etc/myapp.conf
Restart=always
```

### Oneshot (Execute once and exit)
```ini
Type=oneshot
ExecStart=/usr/bin/backup-script
RemainAfterExit=yes
```

### Forking (Traditional daemon)
```ini
Type=forking
ExecStart=/usr/bin/daemon --daemonize
PIDFile=/var/run/daemon.pid
```

## Timer Example (Run service periodically)

**Create timer file: /etc/systemd/system/[FILL].timer**
```ini
[Unit]
Description=Run [FILL] service periodically

[Timer]
OnBootSec=5min
OnUnitActiveSec=1h
Persistent=true

[Install]
WantedBy=timers.target
```

**Enable timer:**
```bash
sudo systemctl enable --now [FILL].timer
```

## Notes

[FILL]
