# Chapter 01 — Server Preparation

This is the first chapter of the QoreChain Light Node Guide.

Before installing any software, your server must be correctly configured. This chapter covers VPS provider selection, server creation, SSH access, system updates, and basic firewall setup.

---

## Recommended Server Requirements

The following table shows the minimum values recommended to run a QoreChain Light Node.

| Component | Minimum | Recommended |
|---|---|---|
| Operating System | Ubuntu 24.04 LTS | Ubuntu 24.04 LTS |
| CPU | 2 vCPU | 4 vCPU |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB NVMe SSD |
| Network | 100 Mbps | 1 Gbps |
| Architecture | x86\_64 | x86\_64 |

> Check official QoreChain announcements before preparing your server. Hardware requirements may change as the network evolves.

---

## VPS Provider Selection

Any VPS provider offering Ubuntu 24.04 and SSD storage can be used. The following providers are commonly used by the operator community.

| Provider | Notable Feature |
|---|---|
| DigitalOcean | Simple UI, good documentation, easy onboarding for individual users |
| Hetzner | Competitive pricing, EU and US locations |
| Vultr | Global locations, flexible plans |
| Contabo | High storage capacity for the price |
| OVHcloud | Competitive pricing for European operators |

Choose a provider based on your budget and preferred server location. Avoid providers that throttle bandwidth during peak hours.

> **Note:** This guide was prepared using [DigitalOcean](https://www.digitalocean.com/?refcode=f69c6b528fe5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) as the example VPS provider. Its straightforward interface and fast server creation process make it a suitable option especially for newcomers.
>
> [![DigitalOcean](https://img.shields.io/badge/DigitalOcean-Used%20in%20this%20guide%20%C2%B7%20No%20KYC-0080FF?logo=digitalocean&logoColor=white&style=flat-square)](https://www.digitalocean.com/?refcode=f69c6b528fe5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

---

## Creating Your First Server on DigitalOcean

This guide is intended for users who have never used a VPS before.

### 1. Create a DigitalOcean Account

- Log in to your [DigitalOcean](https://www.digitalocean.com/?refcode=f69c6b528fe5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) account.
- Once in the control panel, click the **Create** button in the top right corner.
- Select **Droplets** from the dropdown menu.

### 2. Choose an Operating System

Under "Choose an image":

- Select **Ubuntu**.
- Choose **Ubuntu 24.04 LTS** as the version.

This guide was prepared on Ubuntu 24.04.

### 3. Choose a Server Plan

Under "Choose Size":

- Select the **Basic** plan.
- Under CPU options, select **Regular (Shared CPU)**.
- Choose a plan with at least **4 GB RAM** and **2 vCPU**.

### 4. Choose a Region

Under "Choose Region", select the data center closest to you. For example:

- Frankfurt
- Amsterdam
- London

Region selection may affect performance but does not change any installation steps.

### 5. Set Authentication Method

Under "Authentication":

For beginners:

- Select **Password**.
- Create a strong root password.

More experienced users may use an SSH Key instead.

### 6. Create the Droplet

Click the **Create Droplet** button at the bottom of the page. Your server will be ready in approximately 1–2 minutes.

### 7. Find Your Server IP Address

After the server is created, your new Droplet will appear in the control panel. An IP address similar to the following will appear next to the server name:

```
123.45.67.89
```

This address is used to connect to your server.

### 8. Connect to Your Server

**For Windows users:**

Open PowerShell and run the following command:

```powershell
ssh root@YOUR_SERVER_IP
```

Example:

```powershell
ssh root@123.45.67.89
```

If prompted with a confirmation on first connection, type `yes` and press Enter. When asked for a password, enter the root password you created.

If login is successful, you are now connected to your server's terminal and can proceed to Light Node installation.

---

## SSH Access

### Generating an SSH Key

If you do not already have an SSH key, generate one with the following command.

**Linux / macOS:**

```bash
ssh-keygen -t ed25519 -C "your@email.com"
```

Press Enter to accept the default file location. The key pair is saved to `~/.ssh/`.

**Windows (PowerShell):**

```powershell
ssh-keygen -t ed25519 -C "your@email.com"
```

The key pair is saved to `C:\Users\YourUsername\.ssh\`.

---

### Recommended: Disable Password Authentication

After confirming SSH key access works, disable password authentication to reduce brute-force risk.

```bash
sed -i 's/^#*PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh
```

Verify you can still connect with your SSH key before closing the current session.

---

## System Update

After connecting, update the package list and upgrade installed packages.

```bash
apt update && apt upgrade -y
```

This may take a few minutes. If prompted to restart services, press Enter to accept the defaults.

Reboot to apply kernel updates.

```bash
reboot
```

Wait approximately 30 seconds, then reconnect via SSH.

---

## Resource Verification

Verify server resources match the plan you purchased.

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

If any value is significantly below the recommended minimum, consider upgrading the plan before continuing.

---

## Basic UFW Firewall Setup

UFW (Uncomplicated Firewall) comes with Ubuntu. Allow only the ports you need.

Allow SSH first — this step is critical. Skipping it may lock you out of the server.

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

> Additional ports required by the Light Node (for example, panel port `8420`) will be opened in a later chapter after Docker is installed and the node is running.

---

## Internet Connectivity Test

Verify the server can reach the internet.

```bash
ping -c 4 google.com
```

Expected output shows four packets sent and received with no packet loss:

```
4 packets transmitted, 4 received, 0% packet loss
```

Verify DNS resolution is also working:

```bash
curl -s https://api.github.com | head -c 100
```

If both commands return expected output, the server has internet access and working DNS.

---

## Pre-Installation Checklist

Verify the following items before moving to the next chapter.

| Check | Expected State |
|---|---|
| Server active | SSH connection working |
| Operating system | Ubuntu 24.04 LTS |
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

The next chapter covers installing Docker and Docker Compose on Ubuntu 24.04, verifying the installation, and preparing the environment for Light Node setup.

---

## Disclaimer

This document is a community-maintained resource. It does not replace official QoreChain documentation. Server requirements, port numbers, and network rules may change as the project evolves. Always verify critical details through official QoreChain sources before proceeding.
