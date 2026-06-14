# QoreChain Light Node Operations

This document is prepared to help operators follow QoreChain Light Node setup and basic operation processes in a structured way.

The goal is to help operators complete the setup, check services, verify panel access, and apply basic troubleshooting steps quickly.

## Operation Scope

- Server requirements
- Light Node setup
- Service status checks
- Panel access
- Log monitoring
- Restart and basic troubleshooting
- Update process
- Operator checklist
- Maintenance notes

## Requirements

| Requirement | Minimum | Recommended |
|---|---|---|
| Operating System | Ubuntu 20.04 | Ubuntu 22.04 |
| CPU | 2 cores | 4 cores |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB SSD |
| Internet | Stable connection | Stable connection |
| Stake | 1000 QOR | 1000 QOR |

Additional requirements:
- Docker
- Docker Compose
- Basic terminal access

## Required Ports

| Port | Service | Direction |
|---|---|---|
| 8420 | Panel (HTTP) | Inbound |
| 22 | SSH | Inbound |

Make sure your server firewall allows inbound traffic on port 8420. If using UFW:

```bash
ufw allow 8420/tcp
```

## Pre-Setup Check

Before starting the setup, check the following items on the server:

| Check | Expected State |
|---|---|
| Server access | SSH connection works |
| Docker | Docker commands run successfully |
| Docker Compose | `docker compose` is available |
| Network access | The server can reach the internet |
| Port 8420 | Open in firewall |
| Stake | The 1000 QOR requirement is met |

## Setup

Download the Light Node files to your server:

```bash
git clone https://github.com/qorechain/qorechain-lightnode.git
cd qorechain-lightnode
```

Start the services:

```bash
docker compose up -d
```

## Service Check

Check the running containers:

```bash
docker ps
```

Expected services:

- qorechain-lightnode-sx
- qorechain-lightnode-ux

If these services appear in the container list, the Light Node has started at the basic level.

## Panel Access

Open the following address in your browser:

```text
http://YOUR_SERVER_IP:8420
```

Replace `YOUR_SERVER_IP` with your own server IP address.

If the panel opens, basic interface access is verified. If it does not open, check the container status first, then review the server firewall and port settings.

## Log Monitoring

Check the main service logs:

```bash
docker logs qorechain-lightnode-sx
```

Follow logs live:

```bash
docker logs -f qorechain-lightnode-sx
```

## Restart

Restart the services:

```bash
docker compose restart
```

After restart, check the services again:

```bash
docker ps
```

## Update Process

Before updating, note the current service state:

```bash
docker ps
```

Pull the latest changes:

```bash
cd qorechain-lightnode
git pull
```

Restart with the updated files:

```bash
docker compose down
docker compose pull
docker compose up -d
```

Verify the services are running after update:

```bash
docker ps
docker logs qorechain-lightnode-sx
```

Before updating, always check official QoreChain announcements for breaking changes or special update instructions.

## Basic Troubleshooting

| Issue | Check | Action |
|---|---|---|
| Panel does not open | Server IP and port | Check `docker ps` and firewall settings |
| Service is not visible | Container list | Run `docker compose up -d` again |
| Logs show errors | SX service logs | Note the error and check again after restart |
| Node does not respond | Server resources | Check CPU, RAM, and disk usage |
| Setup stopped midway | Project directory | Confirm the correct directory, then rerun the command |
| Port 8420 unreachable | Firewall rules | Run `ufw allow 8420/tcp` and verify with `ufw status` |

## Operator Checklist

- Is the server active?
- Are Docker services running?
- Is the panel reachable on port 8420?
- Are SX and UX containers visible in the list?
- Are there repeated errors in the logs?
- Is the stake requirement met?
- Are there any recent official updates that affect operators?

## Maintenance Notes

Light Node processes may change based on QoreChain updates. Before critical actions, check official announcements, the project repository, and community updates.

Before running commands, confirm that you are on the correct server and inside the correct project directory.

## Disclaimer

This document is a community-maintained operations resource. It does not replace official documentation; official sources should be checked for current commands and network rules.
