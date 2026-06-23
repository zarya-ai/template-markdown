# Network Configuration Template

**Network Name:** [FILL]

**Purpose:** [FILL — e.g., Home lab, Server infrastructure]

**Last Updated:** [FILL]

## Network Overview

```
Network: [FILL]
Subnet: [FILL]
Gateway: [FILL]
DNS: [FILL]

Topology:
┌─────────────────────────────────────────┐
│         Internet / WAN                   │
└──────────────────┬──────────────────────┘
                   │
        ┌──────────┴──────────┐
        │   Router/Gateway    │
        │     [FILL]:[FILL]   │
        └──────────┬──────────┘
                   │
    ┌──────────────┼──────────────┐
    │              │              │
┌───────┐    ┌─────────┐    ┌─────────┐
│Server1│    │Server2  │    │Server3  │
│[FILL] │    │[FILL]   │    │[FILL]   │
└───────┘    └─────────┘    └─────────┘
```

## IP Address Scheme

### Subnets

| Subnet    | Network        | Gateway      | DHCP Start   | DHCP End     | Purpose         |
| --------- | -------------- | ------------ | ------------ | ------------ | --------------- |
| [FILL]    | [FILL]         | [FILL]       | [FILL]       | [FILL]       | [FILL]          |
| [FILL]    | [FILL]         | [FILL]       | [FILL]       | [FILL]       | [FILL]          |

### Static IP Assignments

| Hostname           | IP Address | MAC Address       | Function    | Notes       |
| ------------------ | ---------- | ----------------- | ----------- | ----------- |
| [FILL]             | [FILL]     | [FILL]            | [FILL]      | [FILL]      |
| [FILL]             | [FILL]     | [FILL]            | [FILL]      | [FILL]      |
| [FILL]             | [FILL]     | [FILL]            | [FILL]      | [FILL]      |

## Router Configuration

### Netplan (Ubuntu/Debian)

**File: /etc/netplan/01-netcfg.yaml**

```yaml
network:
  version: 2
  renderer: networkd
  
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - [FILL]
      routes:
        - to: 0.0.0.0/0
          via: [FILL]
      nameservers:
        addresses:
          - [FILL]
          - [FILL]
  
  bonds:
    bond0:
      interfaces:
        - eth0
        - eth1
      parameters:
        mode: active-backup
      addresses:
        - [FILL]
```

**Apply configuration:**
```bash
sudo netplan apply
```

### UFW Firewall

**Enable UFW:**
```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

**Allow services:**
```bash
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow [FILL]/tcp
```

**Port forwarding:**
```bash
sudo ufw allow from [FILL] to any port [FILL]
```

### DHCP Server (dnsmasq)

**File: /etc/dnsmasq.conf**

```conf
# DHCP Configuration
dhcp-range=[FILL],[FILL],12h
dhcp-option=option:router,[FILL]
dhcp-option=option:dns-server,[FILL]

# Static DHCP assignments
dhcp-host=AA:BB:CC:DD:EE:FF,[FILL],[FILL],infinite
dhcp-host=[FILL],[FILL]

# DNS
address=/[FILL]/[FILL]
```

## DNS Configuration

**Resolvers:**
- Primary: [FILL]
- Secondary: [FILL]

**Local DNS zones:**
```bash
# /etc/hosts
[FILL] [hostname]
[FILL] [hostname]
```

## VPN Configuration (OpenVPN)

**Server config: /etc/openvpn/server.conf**

```conf
port [FILL]
proto udp
dev tun

ca /etc/openvpn/keys/ca.crt
cert /etc/openvpn/keys/server.crt
key /etc/openvpn/keys/server.key

server [FILL] [FILL]

push "redirect-gateway def1"
push "dhcp-option DNS [FILL]"

keep-alive 10 120
cipher AES-256-GCM

user nobody
group nogroup

persist-key
persist-tun

status /var/log/openvpn-status.log
log /var/log/openvpn.log
verb 3
```

**Enable and start:**
```bash
sudo systemctl enable openvpn@server
sudo systemctl start openvpn@server
```

## Monitoring

**Check network status:**
```bash
ip addr show
ip route show
ss -tlnp
```

**Monitor bandwidth:**
```bash
iftop
nethogs
```

**Test connectivity:**
```bash
ping [FILL]
traceroute [FILL]
nslookup [hostname]
```

## Backup & Restore

**Backup configuration:**
```bash
sudo tar -czf network-config-backup.tar.gz /etc/netplan /etc/network
```

**Restore configuration:**
```bash
sudo tar -xzf network-config-backup.tar.gz -C /
```

## Security Notes

- [FILL]
- [FILL]
- [FILL]

## Troubleshooting

**No internet connection:**
```bash
ip route show
ping 8.8.8.8
```

**DNS not resolving:**
```bash
cat /etc/resolv.conf
nslookup google.com
```

**IP conflict:**
```bash
arp -a
ip addr flush dev eth0
sudo systemctl restart networking
```

## Notes

[FILL]
