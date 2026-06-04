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
- Operator checklist
- Maintenance notes

## Requirements

- VPS or dedicated server, Ubuntu 22.04 recommended
- Docker
- Docker Compose
- 1000 QOR stake
- Stable internet connection
- Basic terminal access

## Pre-Setup Check

Before starting the setup, check the following items on the server:

| Check | Expected State |
|---|---|
| Server access | SSH connection works |
| Docker | Docker commands run successfully |
| Docker Compose | `docker compose` is available |
| Network access | The server can reach the internet |
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

If repeated errors appear, note the exact error text. Checking whether the same error continues after a restart makes troubleshooting easier.

## Restart

Restart the services:

```bash
docker compose restart
```

After restart, check the services again:

```bash
docker ps
```

## Basic Troubleshooting

| Issue | Check | Action |
|---|---|---|
| Panel does not open | Server IP and port | Check `docker ps` and firewall settings |
| Service is not visible | Container list | Run `docker compose up -d` again |
| Logs show errors | SX service logs | Note the error and check again after restart |
| Node does not respond | Server resources | Check CPU, RAM, and disk usage |
| Setup stopped midway | Project directory and service status | Confirm the correct directory, then rerun the command |

## Operator Checklist

For daily or regular checks, use the following questions:

- Is the server active?
- Are Docker services running?
- Is the panel reachable?
- Are SX and UX containers visible in the list?
- Are there repeated errors in the logs?
- Is the stake requirement met?
- Are there any recent official updates that affect operators?

## Maintenance Notes

Light Node processes may change based on QoreChain updates. Before critical actions, it is recommended to check official announcements, the project repository, and community updates.

Before running commands, confirm that you are on the correct server and inside the correct project directory. For restart, update, or cleanup actions, it is useful to note the current service state first.

## Disclaimer

This document is a community-maintained operations resource. It does not replace official documentation; official sources should be checked for current commands and network rules.
