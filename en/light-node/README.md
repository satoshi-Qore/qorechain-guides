# Light Node Guide — Start Here

> **Network Status:** QoreChain is currently in the pre-mainnet phase. Values such as RPC endpoints, Chain ID, block rewards, and commission rates will be published in the official documentation at mainnet launch. Do not rely on third-party sources for these details.

This guide covers everything you need to run a QoreChain Light Node — from server preparation to daily operations and troubleshooting.

---

## Scope

This guide covers:

- Server selection and preparation
- Docker-based Light Node setup
- Service management and health checks
- Log monitoring and diagnostics
- Common issues and fixes

This guide does **not** cover validator node setup, staking, or governance participation.

---

## Before You Start

Make sure you have:

- A VPS or server meeting the minimum requirements (see Chapter 01)
- SSH access to the server
- Basic Linux command line knowledge
- Docker familiarity is helpful but not required — all commands are provided

---

## Installation Flow

Follow the chapters in order:

| Step | File | Description |
|------|------|-------------|
| 1 | [Server Preparation](./01-server-preparation.md) | Operating system, firewall, user setup |
| 2 | [Docker Installation](./02-docker-installation.md) | Docker setup and configuration |
| 3 | [Light Node Setup](./03-light-node-setup.md) | Pull image, configure, start node |
| 4 | [Monitoring](./04-monitoring.md) | Health checks, panel access, metrics |
| 5 | [Troubleshooting](./05-troubleshooting.md) | Common errors and fixes |

---

## Daily Checks

Once your node is running, check it every day:

```bash
# Check service status
docker ps | grep qorechain

# View recent logs (last 50 lines)
docker logs --tail 50 qorechain-light-node

# Check sync status (if RPC is enabled)
curl -s http://localhost:<RPC_PORT>/status | jq .result.sync_info
```

> Replace `<RPC_PORT>` with the port defined in your node configuration.

---

## Log Monitoring and Troubleshooting

If you notice a problem, start with the logs:

```bash
# Follow live logs
docker logs -f qorechain-light-node

# Check container restart count
docker inspect qorechain-light-node | grep RestartCount
```

For systematic troubleshooting, see [Chapter 05 — Troubleshooting](./05-troubleshooting.md).

---

## Task Proof Note

If you need to submit proof of a running node (for a campaign or task):

- `docker ps` screenshot showing the container is running
- Monitoring panel screenshot (see Chapter 04)
- Log output showing block synchronization progress

---

## Official Sources

Always verify configuration values from official QoreChain sources:

- **Website:** [qorechain.io](https://qorechain.io)
- **GitHub:** [github.com/QoreChain](https://github.com/QoreChain)
- **Discord:** Official announcements channel

> ⚠️ Specific values (RPC URL, Chain ID, genesis file URL, reward rates) are **not hardcoded** in this guide because they may change before mainnet. Always use the most current official values.
