# QoreChain Knowledge Base

This document collects common basic questions about QoreChain and Light Node operations.

## General Questions

### What is QoreChain?

QoreChain is a Layer 1 blockchain focused on post-quantum security, long-term resilience, and cross-network infrastructure.

### Is this repository official?

No. This repository is an independent community resource. Official QoreChain sources and current announcements should be checked for critical steps.

### Who is this document for?

This document is prepared for users following the QoreChain ecosystem, operators who want to run a Light Node, and community members who want quick explanations of basic concepts.

## Light Node Questions

### What is a Light Node?

A Light Node helps relay network traffic, serves network requests, and can earn a portion of network fees.

### Do I need technical knowledge to run a Light Node?

Basic terminal usage, Docker commands, and server access knowledge are needed. Even when setup steps are simple, operators should be able to check service status and logs.

### Which address opens the panel?

The panel is usually opened through the server IP address and the related port:

```text
http://YOUR_SERVER_IP:8420
```

Replace `YOUR_SERVER_IP` with your own server IP address.

## Stake Questions

### Why is 1000 QOR required?

The 1000 QOR stake requirement helps reduce Sybil attacks and aligns operators with the success of the network.

### Is the 1000 QOR a fee?

No. It is not a fee. It is a stake amount that remains locked while the node operates.

### Can the stake be withdrawn?

Yes. The stake can be withdrawn after the node is shut down and the required network rules are completed.

## Operation Questions

### How do I check whether the node is running?

On the server, check the container status:

```bash
docker ps
```

If the expected services appear in the list, the node can be considered running at the basic level.

### How do I check logs?

For the main service logs:

```bash
docker logs qorechain-lightnode-sx
```

For live log monitoring:

```bash
docker logs -f qorechain-lightnode-sx
```

### What should I check first if the panel does not open?

Check the container status first. If the services are running, review the server IP address, port, and firewall settings.

## Note

This knowledge base is prepared for short answers. For more detailed operation steps, follow the [Light Node Operations](./light-node-operations.md) document.
