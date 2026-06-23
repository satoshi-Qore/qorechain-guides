# Chapter 05 — Troubleshooting

This is the fifth chapter of the QoreChain Light Node Guide.

This chapter covers the most common problems encountered when running a QoreChain Light Node, along with diagnostic steps and fixes for each.

---

## Diagnostic Commands

Before diving into specific issues, the following commands are useful starting points for any problem.

**Check container status:**

```bash
cd /opt/qorechain-lightnode
docker compose ps
```

**View recent logs:**

```bash
docker compose logs --tail=100
```

**Check disk space:**

```bash
df -h /
```

**Check memory:**

```bash
free -h
```

**Check Docker service:**

```bash
systemctl status docker
```

---

## Container Exits Immediately After Starting

**Symptom:** `docker compose ps` shows a container with `exited` status shortly after running `docker compose up -d`.

**Diagnosis:**

```bash
docker compose logs qorechain-lightnode-sx
```

Look for error messages near the end of the output.

**Common causes and fixes:**

| Cause | Fix |
|---|---|
| Missing or invalid `.env` value | Open `.env` and verify all required fields are filled in correctly |
| Incorrect RPC endpoint URL | Check the official QoreChain documentation for the current RPC endpoint |
| Port already in use | Run `ss -tlnp \| grep 8420` to check if another process is using the port |
| Wallet address format error | Verify the wallet address format matches what QoreChain expects |

After fixing the issue, restart the containers:

```bash
docker compose down
docker compose up -d
```

---

## Cannot Access the Web Panel

**Symptom:** `http://YOUR_SERVER_IP:8420` returns a connection error or does not load.

**Step 1 — Confirm the container is running:**

```bash
docker compose ps
```

If the panel container is not running, start it and check logs for errors.

**Step 2 — Check UFW firewall:**

```bash
ufw status verbose
```

If port 8420 is not listed, add it:

```bash
ufw allow 8420/tcp
```

**Step 3 — Check provider-level firewall:**

Many VPS providers have a network firewall separate from UFW in their dashboard. Log in to your provider's control panel and confirm that port 8420 is open inbound.

**Step 4 — Confirm the port binding:**

```bash
ss -tlnp | grep 8420
```

Expected output includes a line showing the process listening on `0.0.0.0:8420` or `:::8420`. If nothing appears, the container is not exposing the port correctly — check `docker-compose.yml` for the port mapping.

---

## Node Is Not Syncing

**Symptom:** The panel shows the node is running but block height is not increasing, or logs show repeated connection errors.

**Step 1 — Check internet connectivity:**

```bash
ping -c 4 google.com
curl -s https://api.github.com | head -c 50
```

**Step 2 — Verify the RPC endpoint:**

Confirm the `RPC_ENDPOINT` value in `.env` is correct and reachable:

```bash
curl -s YOUR_RPC_ENDPOINT_URL
```

Replace `YOUR_RPC_ENDPOINT_URL` with the value from your `.env` file. If it returns an error or no output, the endpoint may be down or incorrect.

**Step 3 — Restart the node:**

```bash
docker compose restart
```

Wait two to three minutes and check if the block height begins increasing in the panel.

**Step 4 — Update the node:**

If the network has been updated and your node version is outdated, it may fail to sync:

```bash
git pull
docker compose pull
docker compose up -d
```

---

## Docker Command Not Found

**Symptom:** Running any `docker` command returns `command not found`.

**Fix:** Docker is not installed or the PATH is not set correctly. Return to [Chapter 02 — Docker Installation](./02-docker-installation.md) and reinstall Docker.

If Docker was recently installed, try logging out and back in, then retry the command.

---

## Permission Denied Running Docker

**Symptom:** Docker commands return `permission denied` when run without `sudo`.

**Cause:** The current user is not in the `docker` group.

**Fix:** Add the user to the docker group (replace `YOUR_USERNAME`):

```bash
usermod -aG docker YOUR_USERNAME
```

Log out and back in, then verify:

```bash
docker run hello-world
```

If you are running as `root`, this issue does not apply — all Docker commands work without sudo for root.

---

## Disk Space Full

**Symptom:** Containers crash or refuse to start; `df -h /` shows 100% usage.

**Step 1 — Identify large files:**

```bash
du -sh /opt/qorechain-lightnode/*
docker system df
```

**Step 2 — Clean Docker resources:**

```bash
docker system prune -f
```

**Step 3 — Check log file sizes:**

If log files are large, configure log rotation as described in [Chapter 04 — Monitoring and Maintenance](./04-monitoring.md).

**Step 4 — Expand disk if needed:**

If cleaning is not sufficient, consider upgrading the server plan to increase disk capacity.

---

## Containers Restart Continuously

**Symptom:** `docker compose ps` shows containers with `restarting` status; the node never stays up.

**Diagnosis:**

```bash
docker compose logs --tail=50
```

Look for a repeated error pattern. A container restarting in a loop typically means it starts, encounters a fatal error, exits, and Docker automatically restarts it due to the restart policy.

**Common causes:**

- Corrupted or missing configuration in `.env`
- Network connectivity issue preventing the node from reaching the RPC endpoint
- Resource exhaustion (check `free -h` and `df -h /`)

Fix the underlying cause, then restart cleanly:

```bash
docker compose down
docker compose up -d
```

---

## SSH Connection Refused After Reboot

**Symptom:** After a server reboot, SSH connections are refused.

**Cause:** If password authentication was disabled and the SSH key is missing or incorrect, access is blocked.

**Resolution:** Log in to your VPS provider's dashboard and use their emergency console or rescue mode to access the server. From there you can restore SSH key access or re-enable password authentication temporarily.

> This is why it is critical to verify SSH key access before disabling password authentication (covered in Chapter 01).

---

## Getting Further Help

If the steps in this chapter do not resolve your issue:

1. Search the [qorechain-guides issues](https://github.com/satoshi-Qore/qorechain-guides/issues) for similar reports.
2. Open a new issue with the following information:
   - Your server OS and version (`lsb_release -a`)
   - Docker version (`docker --version`)
   - Output of `docker compose ps`
   - Relevant lines from `docker compose logs`

---

## Disclaimer

This document is a community-maintained resource. It does not replace official QoreChain documentation. Error messages and behavior may vary depending on the node version and network state. Always verify critical details through official QoreChain sources before proceeding.
