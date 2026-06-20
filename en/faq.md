# QoreChain FAQ

This FAQ collects short answers to common QoreChain community questions. It is prepared as an independent community resource and does not replace official QoreChain documentation or announcements.

New to QoreChain? A Getting Started Guide is being prepared.

---

## General

### What is QoreChain?

QoreChain is a Layer 1 blockchain project focused on post-quantum security, multi-VM execution, AI-native infrastructure, and cross-network blockchain architecture.

### Is this repository official?

No. This repository is community-maintained. For critical decisions, network parameters, releases, and mainnet-related details, users should always check official QoreChain sources.

### Why does QoreChain focus on post-quantum security?

Post-quantum security addresses long-term cryptographic risks that may become more important as quantum computing develops. In blockchain systems, this topic is relevant because signatures, keys, and transaction authorization depend heavily on cryptographic assumptions.

### What is the QOR token?

QOR is the native token of the QoreChain network. It is used for staking (required to run a Light Node), transaction fees, and governance participation.

---

## Light Node

### What is a Light Node?

A Light Node is a lightweight network participant that can help with network access, request handling, and operator-side availability. Exact operational requirements should be checked against current official QoreChain instructions.

### What hardware do I need?

A small VPS is sufficient. Minimum: Ubuntu 22.04+, 2 CPU cores, 4 GB RAM, 50 GB SSD, Docker, Docker Compose. See [Light Node Guide](./light-node/) for the full guide.

### Do Light Node operators receive rewards?

Light Node operation appears as part of QoreChain ecosystem tasks and point-based activities. Any real token reward, commission, or mainnet incentive details should be confirmed through official announcements.

### What should I check if my Light Node panel does not open?

Start with basic checks:

1. Confirm the server is online.
2. Confirm the Light Node service or container is running.
3. Check whether the correct IP address and port (8420) are being used.
4. Review firewall settings: `ufw status` — port 8420 must be allowed.
5. Check logs for startup or connection errors.

A Troubleshooting guide is being prepared.

### How do I update my Light Node?

```bash
cd qorechain-lightnode
git pull
docker compose down
docker compose pull
docker compose up -d
```

Always check official QoreChain announcements before updating.

---

## Tasks and Proof

### What should I submit for tasks that do not generate a proof link?

If a task does not generate a direct proof link, submit the most relevant public link available and write a clear short description of what you completed. If the platform allows screenshots, include a screenshot as supporting proof.

### Can I submit community-created guides as proof?

Only if the task requirements match the content you created. A guide, post, issue, or pull request should be relevant to the specific task being submitted.

### Should I claim mainnet results before mainnet is live?

No. Mainnet-specific claims should be avoided until the network is live and official details are available. Use neutral wording such as pre-mainnet preparation, learning notes, or community documentation.

---

## Contribution

### How can I contribute to this repository?

You can suggest corrections, add missing explanations, improve bilingual alignment, or contribute practical setup and troubleshooting notes. See [CONTRIBUTING.md](../CONTRIBUTING.md).

### How do I request a new documentation page?

Use the [Content Request issue template](../.github/ISSUE_TEMPLATE/content-request.md).

### How do I request a translation?

Use the [Translation Request issue template](../.github/ISSUE_TEMPLATE/translation-request.md).

### Can I contribute in Turkish?

Yes. Turkish content belongs in the `tr/` folder. The repository is fully bilingual. See docs/translation-status.md for current coverage.

### What style should new content follow?

Keep content short, practical, neutral, and easy to verify. Avoid promotional claims, unsupported reward statements, and mainnet assumptions. See [STYLE_GUIDE.md](../STYLE_GUIDE.md).
