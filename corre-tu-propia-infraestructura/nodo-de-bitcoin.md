---
icon: bitcoin
---

# Nodo de Bitcoin

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="375"><figcaption><p>Sincronizando un nodo de bitcoin</p></figcaption></figure>

Correr tu propia infraestructura Bitcoin no solo es útil: **es una declaración radical de soberanía digital**. En esta sección aprenderás a correr tu propio nodo de Bitcoin e indexarlo con Esplora, utilizando `docker-compose` y asegurándote de que todo corra sobre almacenamiento sólido y fiable.

Utilizaremos el repositorio [`explorador_sigiloso`](https://github.com/josemariasosa/explorador-sigiloso) como base para desplegar la infraestructura.

#### 🔧 ¿Qué componentes incluye?

La infraestructura que implementaremos consta de:

* 🟠 **Nodo de Bitcoin Core**

### ⚙️ Requisitos para correr tu nodo de Bitcoin

Para levantar la infraestructura completa de **Bitcoin Core** junto con el indexador **Esplora**, necesitas lo siguiente:

**📦 Almacenamiento recomendado**

* 🟢 **Bitcoin Core** (cadena principal): 500 GB
* 🔵 **Esplora** (Electrs + backend): \~300 GB
* ⚠️ **Total sugerido**: **1 TB SSD** (formateado en EXT4 si usas Linux)

**🛠 Requisitos previos**

* Tener **Docker** y **Docker Compose** instalados
* Acceso a una máquina Linux (puede ser física o una VM)
* Conexión estable a Internet (se descargará toda la blockchain de Bitcoin)

### 🏗️ Levantar la Infraestructura

#### 1. 🌞 Clona el repositorio del Explorador Sigiloso

y corre el nodo Bitcoin, asegurándote de que Docker esté corriendo.

```bash
$ git clone https://github.com/josemariasosa/explorador-sigiloso.git
$ cd explorador-sigiloso
```

#### 2. Revisar el archivo Docker Compose

Var una revisada al archivo **docker-compose.yml,** y asegurarse que el volumen sea el correcto, en donde hemos de almacenar el nodo de Bitcoin.

```yaml
  bitcoin:
    image: bitcoin/bitcoin:latest
    container_name: bitcoin-mainnet
    restart: unless-stopped
    ports:
      - "8332:8332"  # RPC
      - "8333:8333"  # P2P
    volumes:
      - /media/honey/bitcoin_data/bitcoin-node:/home/bitcoin/.bitcoin
```

#### 3. Revisar el archivo bitcoin de Configuración

El archivo **bitcoin.conf** deberá estar presente en el directorio del volumen.

```bash
$ sudo ls /media/honey/bitcoin_data/bitcoin-node

banlist.json  blocks      default            mempool.dat
bitcoin.conf  chainstate  fee_estimates.dat  peers.dat
bitcoind.pid  debug.log   indexes            settings.json
```

Y su contenido luce así.

```bash
$ sudo cat /media/honey/bitcoin_data/bitcoin-node/bitcoin.conf

# General options
txindex=1
rpcuser=bitcoin
rpcpassword=bitcoin123
rpcbind=0.0.0.0
rpcallowip=0.0.0.0/0
printtoconsole=1

# Load the default wallet at startup
wallet=default
```

#### 4. 💳 Confirmar la Wallet con bitcoin-cli

Para que un nodo de bitcoin pueda ser consultado, incluso si no está completamente sincronizado, necesita tener cargada una wallet. En el archivo **bitcoin.conf,** añadimos una wallet default, o predeterminada.

Para asegurarse de que la wallet está cargada, es posible ejecutar comandos directamente al nodo mente el `bitcoin-cli`.

```bash
# Listar wallets disponibles
$ docker exec -it bitcoin-mainnet bitcoin-cli \
    -rpcuser=bitcoin \
    -rpcpassword=bitcoin123 \
    listwallets

[
  "default"
]

# Info adicional de la wallet
$ docker exec -it bitcoin-mainnet bitcoin-cli \
    -rpcuser=bitcoin \
    -rpcpassword=bitcoin123 \
    getwalletinfo

{
  "walletname": "default",
  "walletversion": 169900,
  "format": "sqlite",
  "balance": 0.00000000,
  ...
}
```

Si no añadimos el archivo `bitcoin.conf` entonces podemos crear la wallet directamente desde la terminal.

```bash
# Crear la wallet si no existe
$ docker exec -it bitcoin-mainnet bitcoin-cli \
    -rpcuser=bitcoin \
    -rpcpassword=bitcoin123 \
    createwallet default
```

#### 5. Listos para correr el nodo de Bitcoin

Si es la primera vez que se corre, el nodo comenzará a sincronizarse desde cero, este proceso es muy tardado, y se verá en la terminal el avance, mediante los **logs** de Docker.

```bash
$ docker compose up -d bitcoin
$ docker logs -f bitcoin-mainnet

# Para detener el nodo, SIEMPRE utilizar el comando
$ docker compose down
```

#### 6. ☎️ Llamar a nuestro nodo local

Verifica que tu nodo funciona:

```bash
# Obtener detalles de la cadena
$ docker exec -it bitcoin-mainnet bitcoin-cli \
    -rpcuser=bitcoin \
    -rpcpassword=bitcoin123 \
    getblockchaininfo

{
  "chain": "main",
  "blocks": 613236,
  "headers": 893552,
  "bestblockhash": "000000000000000000030bdf3d6c86419b1a42319efa530147d2e793f6592bcc",
  ...
}
```

Para obtener el último bloque, e información adicional sobre el mismo, entonces llamar:

```bash
# Obtener el último bloque
$ docker exec -it bitcoin-mainnet bitcoin-cli \
    -rpcuser=bitcoin \
    -rpcpassword=bitcoin123 \
    getbestblockhash

0000000000000000000b70857493d5c8ab06fbe7a00ba3b45812b45c94df4adf

# Obtener detalles del bloque
$ docker exec -it bitcoin-mainnet bitcoin-cli \
    -rpcuser=bitcoin \
    -rpcpassword=bitcoin123 \
    getblock 0000000000000000000b70857493d5c8ab06fbe7a00ba3b45812b45c94df4adf 2
    
{
  "hash": "0000000000000000000b70857493d5c8ab06fbe7a00ba3b45812b45c94df4adf",
  "confirmations": 16,
  "height": 613255,
  "version": 536870912,
  "versionHex": "20000000",
  "merkleroot": "16c916e623811beb5892d21a1cada8c1bdc64b97d6e08d78016d08352b3e7631",
  "time": 1579257023,
  "mediantime": 1579250177,
  "nonce": 295860742,
  ...
}
```

<figure><img src="../.gitbook/assets/image.png" alt="" width="375"><figcaption><p>Patzcuaro Michoacan</p></figcaption></figure>

### 🌳 Filosofía del Nodo Sigiloso

En Nodo Sigiloso, correr un nodo no es un hobby: es una convicción. Creemos que ser parte de la red es el siguiente paso lógico para un bitcoiner que ya no solo quiere "hodlear", sino participar en la infraestructura misma.

Este documento es bitácora, manual, guía de supervivencia. Ayúdanos a poblar el bosque de nodos soberanos. Correr tu propio nodo no te da solo control: te da conocimiento, privacidad, y dignidad digital.
