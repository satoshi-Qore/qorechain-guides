# Light Node Guide — Start Here

> **Network Status:** QoreChain is in pre-mainnet phase. Specific values for RPC endpoints, Chain ID, block rewards, and commission rates will be published in the official documentation when mainnet launches. Do not rely on third-party sources for these values.

This guide covers everything you need to run a QoreChain Light Node — from server preparation to daily operations and troubleshooting.

---

## Scope

This guide covers:

- Server selection and preparation
- Docker-based Light Node installation
- Service management and health checks
- Log monitoring and diagnostics
- Common issues and their solutions

This guide does **not** cover validator node setup, staking, or governance participation.

---

## Before You Start

Make sure you have:

- A VPS or dedicated server meeting the minimum requirements (see Chapter 01)
- SSH access to your server
- Basic familiarity with Linux command line
- Docker knowledge is helpful but not required — all commands are provided

---

## Setup Flow

Follow the chapters in order:

| Step | File | Description |
|------|------|-------------|
| 1 | [Server Preparation](./01-server-preparation.md) | OS setup, firewall, user config |
| 2 | [Docker Installation](./02-docker-installation.md) | Install and configure Docker |
| 3 | [Light Node Setup](./03-light-node-setup.md) | Pull image, configure, start node |
| 4 | [Monitoring](./04-monitoring.md) | Health checks, panel access, metrics |
| 5 | [Troubleshooting](./05-troubleshooting.md) | Common errors and fixes |

---

## Daily Checks

Once your node is running, verify these each day:

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

## Logs and Troubleshooting

If something looks wrong, start with logs:

```bash
# Follow live logs
docker logs -f qorechain-light-node

# Check container restart count
docker inspect qorechain-light-node | grep RestartCount
```

For systematic troubleshooting, see [Chapter 05 — Troubleshooting](./05-troubleshooting.md).

---

## Proof / Task Note

If you need to submit proof of a running node (for a campaign or task):

- Screenshot of `docker ps` output showing the container running
- Screenshot of the monitoring panel (see Chapter 04)
- Log output showing block sync progress

---

## Official Sources

Always verify configuration values from official QoreChain sources:

- **Website:** [qorechain.io](https://qorechain.io)
- **GitHub:** [github.com/QoreChain](https://github.com/QoreChain)
- **Discord:** Official announcements channel

> ⚠️ Specific values (RPC URL, Chain ID, genesis file URL, reward rates) are **not hardcoded** in this guide because they are subject to change before mainnet. Always use the latest official values.
