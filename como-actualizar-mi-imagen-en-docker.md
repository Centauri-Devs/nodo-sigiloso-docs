---
description: Para nodos de bitcoin corriendo en contenedores de docker
---

# Cómo actualizar mi imagen en docker

Esta vez, joven, señor, señorita, les venimos ofreciendo esto que es el paso a paso pues. Que agarro y que le digo, para correr la versión, la imagen de bitcoin en docker, más actualizada.

#### 🛑 Step 1: Stop the node

This stops the container but preserves data (assuming you're using a persistent volume):

```bash
docker stop bitcoin-mainnet
```

***

#### 🔼 Step 2: Pull the latest Bitcoin Core image

This downloads the latest `bitcoin/bitcoin` image (even if tagged as `latest`, Docker won't auto-update unless you pull it):

```bash
docker pull bitcoin/bitcoin:latest
```

***

#### 🧼 Step 3: Remove the old container

The container is just a wrapper — this **won’t delete** your blockchain data if you're using a volume (double-check your `docker-compose.yml` to confirm this):

```bash
docker rm bitcoin-mainnet
```

***

#### 🚀 Step 4: Restart the node with the new image

If you use `docker-compose.yml`, simply run:

```bash
docker-compose up -d
```

Or if you’re using `docker run`, re-run it with your original settings and volume mounts, something like:

```bash
bashCopyEditdocker run -d \
  --name=bitcoin-mainnet \
  -p 8332:8332 \
  -p 8333:8333 \
  -v /your/host/bitcoin-data:/bitcoin/.bitcoin \
  --restart unless-stopped \
  bitcoin/bitcoin:latest \
  bitcoind -printtoconsole -server
```

***

#### ✅ Step 5: Confirm it’s running and synced

Check logs:

```bash
bashCopyEditdocker logs -f bitcoin-mainnet
```

Or get block height:

```bash
bashCopyEditdocker exec bitcoin-mainnet bitcoin-cli getblockcount
```

***
