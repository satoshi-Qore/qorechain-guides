# Chapter 01 — Server Preparation

This is the first chapter of the QoreChain Light Node Guide.

Before installing any software, you need a properly configured server. This chapter walks through choosing a VPS provider, creating a server, connecting via SSH, applying system updates, and setting up a basic firewall.

---

## Recommended Server Requirements

The following specifications are the recommended minimum baseline for running a QoreChain Light Node.

| Component | Minimum | Recommended |
|---|---|---|
| Operating System | Ubuntu 24.04 LTS | Ubuntu 24.04 LTS |
| CPU | 2 vCPU | 4 vCPU |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB NVMe SSD |
| Network | 100 Mbps | 1 Gbps |
| Architecture | x86\_64 | x86\_64 |

> Always check the latest official QoreChain announcements before provisioning. Hardware requirements may change as the network evolves.

---

## VPS Provider Selection

Any VPS provider that offers Ubuntu 24.04 and SSD-backed storage is suitable. The following are commonly used by the operator community.

| Provider | Notable For |
|---|---|
| Hetzner | Cost-effective, EU and US locations |
| DigitalOcean | Simple UI, well-documented |
| Vultr | Global locations, flexible plans |
| Contabo | High storage per dollar |
| OVHcloud | European operator-friendly pricing |

Choose a provider based on your budget and preferred server location. Avoid providers that throttle network bandwidth during peak hours.

---

## Creating an Ubuntu 24.04 Server

The exact steps vary by provider, but the general flow is the same.

1. Log in to your VPS provider's dashboard.
2. Click **Create** or **Deploy New Server**.
3. Select **Ubuntu 24.04 LTS** as the operating system.
4. Choose a plan that meets the minimum requirements above.
5. Set your **authentication method** — SSH key is strongly recommended over password.
6. Assign a server hostname (for example: `qorechain-lightnode`).
7. Click **Deploy** and wait for the server to become active (usually under two minutes).

Once the server is active, note down the **public IP address**. You will use it in the next step.

---

## SSH Connection

### Generating an SSH Key

If you do not already have an SSH key, generate one with the following command.

**Linux / macOS:**

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

Press Enter to accept the default file location. The key pair is saved to `~/.ssh/`.

**Windows (PowerShell):**

```powershell
ssh-keygen -t ed25519 -C "your-email@example.com"
```

The key pair is saved to `C:\Users\YourUsername\.ssh\`.

---

### Connecting to the Server

Replace `YOUR_SERVER_IP` with your actual server IP address.

**Linux / macOS:**

```bash
ssh root@YOUR_SERVER_IP
```

**Windows (PowerShell or Windows Terminal):**

```powershell
ssh root@YOUR_SERVER_IP
```

On first connection, you will see a fingerprint confirmation prompt:

```
The authenticity of host 'YOUR_SERVER_IP' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

Type `yes` and press Enter.

---

### Recommended: Disable Password Authentication

After confirming SSH key access works, disable password authentication to reduce brute-force risk.

```bash
sed -i 's/^#*PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh
```

Verify that you can still connect via SSH key before closing the current session.

---

## System Updates

After connecting, update the package lists and upgrade installed packages.

```bash
apt update && apt upgrade -y
```

This may take a few minutes. If a prompt asks about restarting services, press Enter to accept the defaults.

Reboot the server to apply any kernel updates.

```bash
reboot
```

Wait about 30 seconds, then reconnect via SSH.

---

## Resource Verification

Confirm the server resources match what you provisioned.

**Check CPU core count:**

```bash
nproc
```

**Check available memory:**

```bash
free -h
```

**Check disk space:**

```bash
df -h /
```

**Check OS version:**

```bash
lsb_release -a
```

Expected output for the OS check:

```
Description:    Ubuntu 24.04 LTS
```

If any value is significantly below the recommended baseline, consider upgrading the plan before proceeding.

---

## Basic UFW Firewall Setup

UFW (Uncomplicated Firewall) is included with Ubuntu. Enable it and allow only the ports you need.

Allow SSH first — this is critical. Do not skip this step or you will lock yourself out.

```bash
ufw allow ssh
```

Enable the firewall:

```bash
ufw enable
```

Check the current firewall status:

```bash
ufw status verbose
```

Expected output:

```
Status: active
To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
```

> Additional ports required by the Light Node (such as the panel port `8420`) will be opened in a later chapter after Docker is installed and the node is running.

---

## Internet Connectivity Test

Confirm the server can reach the internet.

```bash
ping -c 4 google.com
```

Expected output shows four packets sent and received with no packet loss:

```
4 packets transmitted, 4 received, 0% packet loss
```

Also confirm DNS resolution is working:

```bash
curl -s https://api.github.com | head -c 100
```

If both commands return expected output, the server has internet access and DNS is functioning correctly.

---

## Pre-Installation Checklist

Before moving to the next chapter, verify the following items.

| Check | Expected State |
|---|---|
| Server active | SSH connection works |
| OS version | Ubuntu 24.04 LTS |
| CPU | 2+ cores confirmed |
| RAM | 4 GB+ confirmed |
| Disk | 50 GB+ free space |
| System updated | `apt update && apt upgrade -y` completed |
| Firewall active | UFW enabled, SSH allowed |
| Internet access | Ping and curl returned expected output |

If all items pass, the server is ready for the next step.

---

## Next Chapter

**[Chapter 02 — Docker Installation](./02-docker-installation.md)**

The next chapter covers installing Docker and Docker Compose on Ubuntu 24.04, verifying the installation, and preparing the environment for the Light Node setup.

---

## Disclaimer

This document is a community-maintained resource. It does not replace official QoreChain documentation. Server requirements, port numbers, and network rules may change as the project evolves. Always verify critical details through official QoreChain sources before proceeding.
