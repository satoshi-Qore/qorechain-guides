# Chapter 03 — Light Node Setup

This is the third chapter of the QoreChain Light Node Guide.

With Docker installed and the server prepared, this chapter covers cloning the Light Node repository, configuring environment variables, starting the containers, and verifying that the node is running correctly.

---

## Prerequisites

Before starting, confirm that Chapter 02 is complete:

| Check | Expected State |
|---|---|
| Docker installed | `docker --version` returns a version string |
| Docker Compose installed | `docker compose version` returns a version string |
| Docker service enabled | `systemctl is-enabled docker` returns `enabled` |
| Docker service running | `systemctl status docker` shows `active (running)` |

If any item is missing, return to [Chapter 02 — Docker Installation](./02-docker-installation.md) before continuing.

---

## Install Git

The Light Node repository is cloned using Git. Install it if not already present.

```bash
apt-get install -y git
```

Verify the installation:

```bash
git --version
```

Expected output:

```
git version 2.x.x
```

---

## Clone the Light Node Repository

Navigate to the directory where you want to store the node files. The `/opt` directory is a common choice for server applications.

```bash
cd /opt
```

Clone the repository:

```bash
git clone https://github.com/satoshi-Qore/qorechain-lightnode.git
```

Enter the cloned directory:

```bash
cd qorechain-lightnode
```

List the contents to confirm the clone was successful:

```bash
ls -la
```

You should see files including `docker-compose.yml` and a `.env.example` file.

---

## Configure Environment Variables

The Light Node reads its configuration from a `.env` file. Copy the example file to create your own:

```bash
cp .env.example .env
```

Open the file for editing:

```bash
nano .env
```

The file contains configuration keys for the node. Update the required values:

| Variable | Description |
|---|---|
| `NODE_NAME` | A display name for your node (any string) |
| `PANEL_PORT` | Port for the web panel (default: `8420`) |
| `RPC_ENDPOINT` | QoreChain RPC endpoint URL |
| `WALLET_ADDRESS` | Your operator wallet address |

> Check the official QoreChain documentation or the repository README for the current list of required variables and valid RPC endpoint URLs.

Save and close the file: press `Ctrl+X`, then `Y`, then `Enter`.

---

## Open the Panel Port

Before starting the node, open the panel port in UFW so you can access the web interface.

```bash
ufw allow 8420/tcp
```

If you changed `PANEL_PORT` in the `.env` file, replace `8420` with your chosen port number.

Verify the firewall rules:

```bash
ufw status verbose
```

Expected output includes a line for port `8420`:

```
8420/tcp                   ALLOW IN    Anywhere
8420/tcp (v6)              ALLOW IN    Anywhere (v6)
```

---

## Start the Light Node

Start all containers defined in the `docker-compose.yml` file in detached mode:

```bash
docker compose up -d
```

Docker will pull the required images on the first run. This may take a few minutes depending on your connection speed.

Expected output (on first run):

```
[+] Pulling images ...
[+] Running 2/2
 ✔ Container qorechain-lightnode-sx    Started
 ✔ Container qorechain-lightnode-ux    Started
```

---

## Verify the Node Is Running

### Check Container Status

```bash
docker compose ps
```

All containers should show `running` status:

```
NAME                       STATUS
qorechain-lightnode-sx     running
qorechain-lightnode-ux     running
```

### View Node Logs

Check the live log output to confirm the node started without errors:

```bash
docker compose logs -f
```

Look for lines indicating a successful connection to the network. Press `Ctrl+C` to exit the log stream.

### Access the Web Panel

Open a browser and navigate to:

```
http://YOUR_SERVER_IP:8420
```

Replace `YOUR_SERVER_IP` with your server's public IP address.

If the panel loads, the node is running and accessible.

---

## Managing the Node

### Stop the Node

```bash
docker compose down
```

### Restart the Node

```bash
docker compose restart
```

### Update the Node

Pull the latest changes from the repository and rebuild the containers:

```bash
git pull
docker compose pull
docker compose up -d
```

---

## Post-Setup Checklist

| Check | Expected State |
|---|---|
| Repository cloned | `/opt/qorechain-lightnode` directory exists |
| `.env` configured | Required variables filled in |
| Port 8420 open | `ufw status` shows `8420/tcp ALLOW` |
| Containers running | `docker compose ps` shows all containers as `running` |
| Logs clean | No error lines in `docker compose logs` |
| Panel accessible | `http://YOUR_SERVER_IP:8420` loads in browser |

If all items pass, the Light Node is running correctly.

---

## Troubleshooting

**Containers exit immediately after starting:**
Run `docker compose logs` and check for configuration errors. The most common cause is a missing or incorrect value in the `.env` file.

**Panel not accessible:**
Confirm port 8420 is open in UFW (`ufw status`) and that no external firewall at the VPS provider level is blocking the port. Some providers have a separate network firewall in their dashboard.

**Cannot clone repository:**
Ensure Git is installed (`git --version`) and the server has internet access (`ping -c 4 github.com`).

---

## Next Chapter

**[Chapter 04 — Monitoring and Maintenance](./04-monitoring.md)**

The next chapter covers setting up log monitoring, configuring alerts, keeping the node updated, and routine maintenance tasks.

---

## Disclaimer

This document is a community-maintained resource. It does not replace official QoreChain documentation. Repository URLs, environment variable names, and port numbers may change as the project evolves. Always verify critical details through official QoreChain sources before proceeding.
