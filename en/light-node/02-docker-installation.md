# Chapter 02 — Docker Installation

This is the second chapter of the QoreChain Light Node Guide.

The QoreChain Light Node runs inside Docker containers. This chapter covers installing Docker Engine and Docker Compose on Ubuntu 24.04, verifying the installation, and preparing the environment before node setup.

---

## Prerequisites

Before starting, confirm that Chapter 01 is complete:

| Check | Expected State |
|---|---|
| Server active | SSH connection works |
| OS version | Ubuntu 24.04 LTS |
| System updated | `apt update && apt upgrade -y` completed |
| Firewall active | UFW enabled, SSH allowed |

If any item is missing, return to [Chapter 01 — Server Preparation](./01-server-preparation.md) before continuing.

---

## Remove Old Docker Versions

Ubuntu may have outdated Docker packages installed under different names. Remove them first to avoid conflicts.

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do
  apt-get remove -y $pkg 2>/dev/null
done
```

If none of these packages are installed, the command exits silently — that is expected.

---

## Install Docker Engine

### Add the Docker Repository

Install the required dependencies:

```bash
apt-get install -y ca-certificates curl
```

Create the directory for apt keyrings:

```bash
install -m 0755 -d /etc/apt/keyrings
```

Download and add the Docker GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc
```

Add the Docker repository to apt sources:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update the package list:

```bash
apt-get update
```

---

### Install Docker Packages

```bash
apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

This installs Docker Engine, the CLI, the container runtime, and the Compose plugin.

---

## Verify the Installation

### Check Docker Version

```bash
docker --version
```

Expected output (version numbers may differ):

```
Docker version 27.x.x, build xxxxxxx
```

### Check Docker Compose Version

```bash
docker compose version
```

Expected output:

```
Docker Compose version v2.x.x
```

### Run the Test Container

```bash
docker run hello-world
```

Expected output includes:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

If this output appears, Docker is installed and working.

---

## Configure Docker to Start on Boot

Enable Docker to start automatically when the server reboots:

```bash
systemctl enable docker
systemctl enable containerd
```

Check that the Docker service is currently running:

```bash
systemctl status docker
```

Expected output shows `Active: active (running)`.

---

## Optional: Run Docker Without sudo

By default, Docker commands require `root` or `sudo`. If you plan to run the node as a non-root user, add that user to the `docker` group.

> Skip this section if you are running everything as `root`.

Replace `YOUR_USERNAME` with the actual username:

```bash
usermod -aG docker YOUR_USERNAME
```

Log out and back in for the group change to take effect, then verify:

```bash
docker run hello-world
```

The command should run without `sudo`.

---

## Post-Installation Checklist

Verify the following before moving to the next chapter.

| Check | Expected State |
|---|---|
| Docker installed | `docker --version` returns a version string |
| Docker Compose installed | `docker compose version` returns a version string |
| hello-world container | Ran successfully |
| Docker service enabled | `systemctl is-enabled docker` returns `enabled` |
| Docker service running | `systemctl status docker` shows `active (running)` |

If all items pass, the environment is ready for Light Node setup.

---

## Next Chapter

**[Chapter 03 — Light Node Setup](./03-light-node-setup.md)**

The next chapter covers cloning the Light Node repository, configuring environment variables, starting the containers, and verifying that the node is running.

---

## Disclaimer

This document is a community-maintained resource. It does not replace official QoreChain documentation. Docker installation steps follow the official Docker documentation for Ubuntu and are accurate as of Ubuntu 24.04 LTS. Always verify critical details through official sources before proceeding.
