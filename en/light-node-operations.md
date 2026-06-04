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
- Operator notes

## Requirements

- VPS or dedicated server, Ubuntu 22.04 recommended
- Docker
- Docker Compose
- 1000 QOR stake
- Stable internet connection
- Basic terminal access

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

If the panel opens, basic interface access is verified.

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

## Basic Troubleshooting

| Issue | Check | Action |
|---|---|---|
| Panel does not open | Server IP and port | Check `docker ps` and firewall settings |
| Service is not visible | Container list | Run `docker compose up -d` again |
| Logs show errors | SX service logs | Note the error and check again after restart |
| Node does not respond | Server resources | Check CPU, RAM, and disk usage |

## Operator Checklist

- Is the server active?
- Are Docker services running?
- Is the panel reachable?
- Are SX and UX containers visible in the list?
- Are there repeated errors in the logs?
- Is the stake requirement met?

## Maintenance Notes

Light Node processes may change based on QoreChain updates. Before critical actions, it is recommended to check official announcements, the project repository, and community updates.

## Disclaimer

This document is a community-maintained operations resource. It does not replace official documentation; official sources should be checked for current commands and network rules.
