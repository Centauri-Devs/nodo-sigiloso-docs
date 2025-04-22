---
icon: bitcoin
---

# Bitcoin

## Corre tu propia infraestructura

Correr tu propia infraestructura Bitcoin no solo es útil: es una declaración radical de soberanía digital. En esta sección aprenderás a correr tu propio nodo de Bitcoin y a indexarlo con Esplora, usando `docker-compose`, y asegurándote de que todo corre sobre almacenamiento sólido y fiable.

> Esta sección se actualizó por última vez el **2025-04-21**.

### 📦 Requisitos de almacenamiento

Para correr la infraestructura completa de Bitcoin + Esplora se recomienda tener:

* 🟢 **Bitcoin Core (cadena principal):** 500 GB
* 🔵 **Esplora indexer (Electrs + esplora backend):** \~300 GB

> ⚠️ Total sugerido: **1 TB de almacenamiento SSD (EXT4 si es en Linux)**

### 🛠 Requerimientos previos

* Docker y Docker Compose
* Acceso a una máquina Linux (VM o física)
* Conexión estable para sincronizar toda la blockchain de Bitcoin

### 🚀 Pasos para levantar la infraestructura

#### 1. Asegurarse de disponer del almacenamiento suficiente

Antes de comenzar, asegúrate de que tienes un SSD montado con suficiente espacio libre. Esto es crítico para correr un nodo Bitcoin confiable.

```
# Verifica tus discos conectados
lsblk

# Verifica el espacio disponible
$ df -h /media/honey/bitcoin_data/
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda        916G  360G  510G  42% /media/honey/bitcoin_data
```

Montaje y desmontaje del SSD:

```
# Montar
sudo mkdir -p /mnt/bitcoin-data
sudo mount /dev/sda /mnt/bitcoin-data

# Desmontar
sudo umount /mnt/bitcoin-data
```

#### 2. Clona el repositorio del Explorador Sigiloso 🌞

y corre el nodo Bitcoin

```
git clone git@github.com:josemariasosa/explorador-sigiloso.git
cd explorador-sigiloso
docker compose up -d bitcoin
```

**¿Qué hace el servicio `bitcoin` del docker-compose?**

Este contenedor levanta una instancia de `bitcoind` (Bitcoin Core) con soporte para:

* `txindex=1`: permite indexar todas las transacciones (clave para exploradores y análisis de bloques)
* `rpcbind=0.0.0.0` y `rpcallowip=0.0.0.0/0`: habilita llamadas RPC externas (útil para explorador)
* `wallet=default`: una wallet por defecto que se carga automáticamente

La configuración se almacena en tu disco montado en `/mnt/bitcoin-data`, y se mantiene independiente del contenedor.

Verifica que tu nodo funciona:

```
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 getblockchaininfo
```

#### 3. Levanta el explorador y la API

```
docker compose up -d --build explorador_api
```

Este servicio corre la API REST que conecta con tu nodo para visualizar información como balances, bloques y transacciones. La puedes consultar así:

```
curl http://localhost:3000/btc/last-block-delta
```

### 🧠 Configuración esencial

Tu archivo `bitcoin.conf` debería estar ubicado en el SSD en `/mnt/bitcoin-data/bitcoin.conf`, y contener:

```
txindex=1
rpcuser=bitcoin
rpcpassword=bitcoin123
rpcbind=0.0.0.0
rpcallowip=0.0.0.0/0
printtoconsole=1
wallet=default
```

Esto asegura que tu wallet se cargue automáticamente en cada arranque del nodo y que la API pueda acceder al RPC.

### 🔧 Comandos útiles para usuarios Bitcoin

```
# Crear la wallet si no existe
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 createwallet default

# Obtener el último bloque
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 getbestblockhash

# Obtener detalles de un bloque
docker exec -it bitcoin-mainnet bitcoin-cli -rpcuser=bitcoin -rpcpassword=bitcoin123 getblock <BLOCK_HASH> 2
```

Consulta vía API:

```
curl http://localhost:3000/btc/balance/1DrK44np3gMKuvcGeFVv9Jk67zodP52eMu
```

### 📤 Cierre y mantenimiento

Antes de apagar tu nodo:

```
docker compose down
sudo umount /mnt/bitcoin-data
sudo shutdown now
```

Si usas Mac y UTM:

```
diskutil unmount /Volumes/bitcoin_data
```

> 🧠 No desconectes el SSD sin desmontarlo. Recuerda que tu nodo es un monje zen: necesita cerrar con paz.

### 🌳 Filosofía del Nodo Sigiloso

En Nodo Sigiloso, correr un nodo no es un hobby: es una convicción. Creemos que ser parte de la red es el siguiente paso lógico para un bitcoiner que ya no solo quiere "hodlear", sino participar en la infraestructura misma.

Este documento es bitácora, manual, guía de supervivencia. Ayúdanos a poblar el bosque de nodos soberanos. Correr tu propio nodo no te da solo control: te da conocimiento, privacidad, y dignidad digital.

> Próximo capítulo: cómo usar la API de `explorador_sigiloso_api` para visualizar bloques, transacciones y balances. 🌐📊
