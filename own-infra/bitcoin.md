---
icon: pen-to-square
---

# Corre tu propia infraestructura

Correr tu propia infraestructura no solo es útil, también es una declaración de soberanía digital. En esta sección aprenderás a levantar tu nodo de Bitcoin y su indexador Esplora, usando `docker-compose`, y lo necesario en almacenamiento.

> Esta sección documenta la ruta `nodosigiloso.com/btc/` y se actualizó por última vez el **2025-04-21**.

## 📦 Requisitos de almacenamiento

Para correr la infraestructura completa de Bitcoin + Esplora se recomienda tener:

- 🟢 **Bitcoin Core (cadena principal):** 500 GB #TODO check updated numbers
- 🔵 **Esplora indexer (Electrs + esplora backend):** ~300 GB

> ⚠️ Total sugerido: **1 TB de almacenamiento SSD (EXT4 si es en Linux)**

## Requerimientos

- Docker

## 🚀 Pasos para levantar la infraestructura

### 1. Asegurarse de disponer del almacenamiento suficiente

Conecta el disco SSD a tu VM o servidor físico. Usa un contenedor temporal para darle formato:

```bash
# Find the correct sdx.
$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda           8:0    0 931.5G  0 disk /media/honey/bitcoin_data
mmcblk0     179:0    0  59.6G  0 disk
|-mmcblk0p1 179:1    0   512M  0 part /boot/firmware
`-mmcblk0p2 179:2    0  59.1G  0 part /

# Check the available storage.
$ df -h /media/honey/bitcoin_data/
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda        916G  360G  510G  42% /media/honey/bitcoin_data
```

Si necesitas montar un disco duro externo, conocido como SSD, te sera util montar y desmontar discos.

```bash
# Montar un disco.
sudo mkdir -p /mnt/bitcoin-data
sudo mount /dev/sda /mnt/bitcoin-data
df -h /mnt/bitcoin-data/

# Desmontar el disco.
sudo umount /mnt/bitcoin-data
```

### 2. Clona el repositorio y corre el nodo Bitcoin

```bash
git clone git@github.com:josemariasosa/explorador-sigiloso.git
cd explorador-sigiloso
docker compose up -d bitcoin
```

Verifica el estado del nodo:

```bash
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 getblockchaininfo
```

### 3. Levanta el explorador y API

```bash
docker compose up -d --build explorador_api
```

Consulta el estado de la blockchain desde tu API local:

```bash
curl http://localhost:3000/btc/last-block-delta
```

## 🧠 Notas de configuración

Asegúrate de tener el archivo `bitcoin.conf` en `/mnt/bitcoin-data/` con el siguiente contenido:

```ini
txindex=1
rpcuser=bitcoin
rpcpassword=bitcoin123
rpcbind=0.0.0.0
rpcallowip=0.0.0.0/0
printtoconsole=1
wallet=default
```

Esto permite que tu wallet se cargue automáticamente cada vez que inicies el nodo.

## 🔧 Comandos útiles

```bash
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 createwallet default
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 getbestblockhash
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 getblock <BLOCK_HASH> 2
```

Consulta desde la API:

```bash
curl http://localhost:3000/btc/balance/1DrK44np3gMKuvcGeFVv9Jk67zodP52eMu
```

## 📤 Cierre y mantenimiento

Antes de apagar tu VM o desconectar el SSD:

```bash
docker compose down
sudo umount /mnt/bitcoin-data
sudo shutdown now
diskutil unmount /Volumes/bitcoin_data
```

> 🧠 No desconectes físicamente el disco sin desmontarlo: puedes perder datos importantes o corromper tu nodo.

## 🌳 Filosofía del Nodo Sigiloso

En Nodo Sigiloso, creemos en descentralizar con acción. Correr tu propia infraestructura es más que técnico: es político, filosófico y divertido.

Esta documentación está pensada como una bitácora personal, pero también como una guía para otrxs. Queremos que más ardillas se unan al bosque.

El próximo capítulo será sobre cómo usar la API de `explorador_sigiloso_api` para crear dashboards y visualizaciones de datos en Bitcoin. ¡Sigue construyendo!


