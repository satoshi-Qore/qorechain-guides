# QoreChain Light Node Setup Guide

## Requirements

* VPS (Ubuntu 22.04 recommended)
* Docker
* Docker Compose
* 1000 QOR stake

## Installation

```bash
git clone https://github.com/qorechain/qorechain-lightnode.git
cd qorechain-lightnode
docker compose up -d
```

## Verify Services

```bash
docker ps
```

Expected services:

* qorechain-lightnode-sx
* qorechain-lightnode-ux

## Dashboard Access

Open your browser and visit:

```text
http://YOUR_SERVER_IP:8420
```

## Troubleshooting

### Check logs

```bash
docker logs qorechain-lightnode-sx
```

### Restart services

```bash
docker compose restart
```

## Notes

This guide is maintained by the community and may be updated as QoreChain evolves.
