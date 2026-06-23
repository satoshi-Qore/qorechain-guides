# QoreChain Light Node Troubleshooting

This guide covers common issues encountered when setting up and operating a QoreChain Light Node, and the steps to resolve them.

For a general overview, see the [Getting Started Guide](./getting-started.md).
For the full operations guide, see the [Light Node Guide](./light-node/).
For step-by-step troubleshooting within the full guide, see [Light Node Guide — Chapter 05](./light-node/05-troubleshooting.md).

---

## Panel Issues

### Panel does not open on port 8420

**Symptoms:** Browser shows connection refused or timeout when accessing `http://YOUR_IP:8420`

**Steps:**

1. Check if containers are running:
   ```bash
   cd /opt/qorechain-light-node
   docker compose ps
   ```
   You should see `qorechain-light-node` and `qorechain-monitor` in the list.

2. If containers are not running, restart:
   ```bash
   docker compose up -d
   ```

3. Check your firewall:
   ```bash
   ufw status
   ```
   If port 8420 is not listed, add it:
   ```bash
   ufw allow 8420/tcp
   ```

4. Check your server provider's security groups or firewall rules — port 8420 must be open for inbound TCP traffic.

5. Make sure you are connecting to your server's **public IP**, not `localhost` or `127.0.0.1`.

### Panel opens but shows errors

**Steps:**

1. Check the node service logs:
   ```bash
   cd /opt/qorechain-light-node
   docker compose logs qorechain-light-node
   ```

2. Look for repeated errors or startup failures.

3. If logs show a crash loop, try a clean restart:
   ```bash
   docker compose down
   docker compose up -d
   ```

---

## Container Issues

### Containers are not visible in `docker compose ps`

**Steps:**

1. Navigate to the project directory:
   ```bash
   cd /opt/qorechain-light-node
   ```

2. Check if any containers are stopped:
   ```bash
   docker compose ps -a
   ```

3. Start the services:
   ```bash
   docker compose up -d
   ```

4. If the above fails, check `docker compose` is available:
   ```bash
   docker compose version
   ```

### Container starts then immediately stops

**Steps:**

1. View recent logs:
   ```bash
   docker compose logs --tail=50 qorechain-light-node
   ```

2. Common causes:
   - Port 8420 already in use by another process
   - Insufficient disk space
   - Missing or incorrect values in the `.env` configuration file

3. Check disk usage:
   ```bash
   df -h /
   ```

---

## Update Issues

### Update did not apply

**Steps:**

1. Make sure you are in the correct directory:
   ```bash
   pwd
   ```
   Should output a path ending in `/qorechain-light-node`

2. Pull the latest changes:
   ```bash
   git pull
   ```

3. Perform a full restart with updated images:
   ```bash
   docker compose down
   docker compose pull
   docker compose up -d
   ```

4. Verify the services are running after update:
   ```bash
   docker compose ps
   docker compose logs --tail=20 qorechain-light-node
   ```

---

## Network and Stake Issues

### Node shows as offline or disconnected

Verify:
- Docker containers are running (`docker compose ps`)
- Port 8420 is reachable from the internet
- Stake requirement (1000 QOR minimum) is met
- No recent official QoreChain announcements about network changes

### Stake check fails

Confirm the wallet address holding 1000 QOR stake is the one registered with the Light Node. Check official QoreChain channels for staking guidance.

---

## General Checks

When in doubt, run through this checklist:

| Check | Command |
|---|---|
| Containers running | `docker compose ps` |
| Node logs | `docker compose logs qorechain-light-node` |
| Firewall status | `ufw status` |
| Disk space | `df -h /` |
| Project directory | `ls /opt/qorechain-light-node/` |

---

## Disclaimer

This guide is a community-maintained resource. Commands and procedures may change with QoreChain updates. Always verify against official sources and announcements before taking action.
