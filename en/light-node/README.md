# Light Node Guide — Start Here

> **Network Status:** QoreChain is currently in pre-mainnet phase. Values such as RPC endpoints, Chain ID, block rewards, and commission rates will be published in official documentation at mainnet launch. Do not rely on third-party sources for these values.

This guide covers everything you need to run a QoreChain Light Node — from server preparation through daily operations and troubleshooting.

---

## Scope

This guide covers:

- Server selection and preparation
- Docker-based Light Node setup
- Service management and health checks
- Log monitoring and diagnostics
- Common issues and solutions

This guide does **not** cover validator node setup, staking, or governance participation.

---

## Before You Start

Make sure you have:

- A VPS or server meeting minimum requirements (see Chapter 01)
- SSH access to the server
- Basic Linux command-line knowledge
- Docker familiarity helps but is not required — all commands are provided

---

## Setup Flow

Follow the chapters in order:

| Step | File | Description |
|------|------|-------------|
| 1 | [Server Preparation](./01-server-preparation.md) | OS, firewall, user setup |
| 2 | [Docker Setup](./02-docker-installation.md) | Docker installation and configuration |
| 3 | [Light Node Setup](./03-light-node-setup.md) | Pull image, configure, start the node |
| 4 | [Monitoring](./04-monitoring.md) | Health checks, panel access, metrics |
| 5 | [Troubleshooting](./05-troubleshooting.md) | Common errors and solutions |

---

## Daily Checks

Once your node is running, check it each day:

```bash
# Check service status
docker compose ps

# View recent logs (last 50 lines)
docker compose logs --tail=50
```

---

## Log Monitoring and Troubleshooting

If you notice a problem, start with the logs:

```bash
# Follow live logs
docker compose logs -f qorechain-lightnode-sx

# Check restart count
docker inspect qorechain-lightnode-sx | grep RestartCount
```

For systematic troubleshooting, see [Chapter 05 — Troubleshooting](./05-troubleshooting.md).

---

## Task Proof Note

If you need to provide proof of a running node (for a campaign or task):

- `docker compose ps` screenshot showing containers running
- Monitoring panel screenshot (see Chapter 04)
- Log output showing block sync progress

---

## Official Sources

Always verify configuration values from official QoreChain sources:

- **Website:** [qorechain.io](https://qorechain.io)
- **GitHub:** [github.com/satoshi-Qore](https://github.com/satoshi-Qore)
- **Discord:** Official announcements channel

> ⚠️ Specific values (RPC URL, Chain ID, genesis file URL, reward rates) are **not hardcoded in this guide** because they may change before mainnet. Always use the most current official values.
