# Chapter 04 — Monitoring and Maintenance

This is the fourth chapter of the QoreChain Light Node Guide.

With the Light Node running, this chapter covers how to monitor node health, manage logs, keep the software updated, and perform routine maintenance tasks to ensure stable long-term operation.

---

## Prerequisites

Before starting, confirm that Chapter 03 is complete:

| Check | Expected State |
|---|---|
| Containers running | `docker compose ps` shows all containers as `running` |
| Panel accessible | `http://YOUR_SERVER_IP:8420` loads in browser |

If any item is missing, return to [Chapter 03 — Light Node Setup](./03-light-node-setup.md) before continuing.

---

## Checking Node Status

### Container Status

Check whether all containers are running at any time:

```bash
cd /opt/qorechain-light-node
docker compose ps
```

All listed containers should show `running` status. If any container shows `exited` or `restarting`, check the logs for that container.

### Resource Usage

Monitor CPU, memory, and network usage of running containers:

```bash
docker stats
```

This displays a live view. Press `Ctrl+C` to exit.

For a one-time snapshot instead of a live view:

```bash
docker stats --no-stream
```

---

## Log Management

### View Live Logs

Stream logs from all containers:

```bash
cd /opt/qorechain-light-node
docker compose logs -f
```

Stream logs from a specific container only:

```bash
docker compose logs -f qorechain-light-node
```

Press `Ctrl+C` to stop the stream.

### View Recent Logs

Show the last 100 lines from all containers:

```bash
docker compose logs --tail=100
```

### Log Rotation

Docker's default logging does not rotate logs automatically, which can cause disk space issues over time. Configure log rotation for each container by adding the following to your `docker-compose.yml` under each service:

```yaml
logging:
  driver: "json-file"
  options:
    max-size: "10m"
    max-file: "5"
```

This limits each log file to 10 MB and keeps a maximum of 5 rotated files per container.

After editing the file, restart the containers to apply the change:

```bash
docker compose down
docker compose up -d
```

---

## Disk Space Monitoring

Check available disk space on the server:

```bash
df -h /
```

Check how much space Docker is using:

```bash
docker system df
```

### Cleaning Up Unused Docker Resources

Remove stopped containers, unused images, and build cache:

```bash
docker system prune -f
```

> This does not remove running containers or volumes attached to active containers.

To also remove unused volumes (use with caution — verify no important data is stored there first):

```bash
docker system prune --volumes -f
```

---

## Updating the Light Node

Keep the node software up to date to receive bug fixes and network compatibility updates.

### Check for Updates

Pull the latest changes from the repository:

```bash
cd /opt/qorechain-light-node
git fetch origin
git status
```

If the output shows `Your branch is behind 'origin/main'`, an update is available.

### Apply the Update

```bash
git pull
docker compose pull
docker compose up -d
```

`docker compose pull` downloads the latest container images. `docker compose up -d` restarts containers using the new images.

Verify the containers are running after the update:

```bash
docker compose ps
```

---

## Restarting After a Server Reboot

If the server was rebooted and the containers did not start automatically, start them manually:

```bash
cd /opt/qorechain-light-node
docker compose up -d
```

To prevent this from happening after future reboots, confirm that Docker is set to start on boot:

```bash
systemctl is-enabled docker
```

Expected output: `enabled`

If it returns `disabled`, enable it:

```bash
systemctl enable docker
```

---

## Backing Up Configuration

The `.env` file contains your node configuration. Back it up to a secure location periodically.

```bash
cp /opt/qorechain-light-node/.env ~/lightnode-env-backup-$(date +%Y%m%d)
```

Store the backup outside the server (for example, in a local file or a password manager) in case the server needs to be rebuilt.

---

## Maintenance Checklist

Run through the following checks periodically to keep the node healthy.

| Task | Recommended Frequency |
|---|---|
| Check container status (`docker compose ps`) | Daily |
| Review recent logs for errors | Daily |
| Check disk space (`df -h /`) | Weekly |
| Run `docker system prune -f` | Weekly |
| Check for repository updates (`git fetch`) | Weekly |
| Apply available updates | As released |
| Backup `.env` file | After any configuration change |

---

## Next Chapter

**[Chapter 05 — Troubleshooting](./05-troubleshooting.md)**

The next chapter covers common errors, container failures, connectivity issues, and steps to recover a node that has stopped syncing or responding.

---

## Disclaimer

This document is a community-maintained resource. It does not replace official QoreChain documentation. Maintenance procedures and update workflows may change as the project evolves. Always verify critical details through official QoreChain sources before proceeding.
