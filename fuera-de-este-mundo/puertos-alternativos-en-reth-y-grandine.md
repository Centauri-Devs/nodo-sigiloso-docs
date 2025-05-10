---
icon: ship
---

# Puertos alternativos en Reth y Grandine

<figure><img src="../.gitbook/assets/image.png" alt="" width="375"><figcaption><p>José María Morelos y Pavón</p></figcaption></figure>

Al correr múltiples clientes de Ethereum en una misma máquina, es importante evitar conflictos de puertos. Aquí documento cómo instalé y configuré **Reth** y **Grandine**, y cómo fui debuggeando para usar puertos alternativos correctamente.

Mi máquina ya se encontraba corriendo el cliente de ejecución [Nethermind](https://www.nethermind.io/nethermind-client) y el cliente de consenso [Nimbus](https://nimbus.team/).

***

### ✅ Instalación de Reth

```bash
# Clonamos el repositorio oficial
git clone https://github.com/paradigmxyz/reth
cd reth/

# Instalamos el binario principal
cargo install --locked --path bin/reth --bin reth
```

{% hint style="info" %}
Los archivos compilados están en `target/release/reth`. Sin embargo, el ejecutable de reth fue instalado también.
{% endhint %}

***

### 🚀 Ejecución con puertos por defecto

```bash
# Puerto por defecto
reth node

# Cambiar solo el puerto de discovery
reth node --discovery.port 30304

# Cambiar ambos puertos
reth node --discovery.port 30304 --port 30304

# También el puerto del authrpc
reth node --discovery.port 30304 --port 30304 --authrpc.port 8552
```

> ⚠️ En todos los casos, el nodo arrancaba sin errores aparentes, pero **no sincronizaba bloques**. Aparentemente, los puertos no estaban abiertos por el firewall del sistema.

***

### 🔩 Instalación de dependencias del sistema

```bash
sudo apt-get install ca-certificates libssl-dev clang cmake unzip protobuf-compiler libz-dev
```

Esto es necesario para compilar correctamente proyectos en Rust como Reth o Grandine.

***

### 🧱 Compilación de Grandine

```bash
git clone https://github.com/grandinetech/grandine
cd grandine/

# Inicializar los submódulos necesarios
git submodule update --init dedicated_executor eth2_libp2p

# Compilar con el perfil compacto y redes por defecto
cargo build --profile compact --features default-networks
```

***

### 🔥 Configuración de puertos con UFW

Para permitir la conexión y sincronización de nodos, hay que abrir los puertos específicos utilizados:

```bash
# Activar el firewall si aún no está activado
sudo ufw enable

# Permitir puertos de red alternativos para Reth
sudo ufw allow 30304/tcp   # P2P TCP
sudo ufw allow 30304/udp   # Discovery UDP
sudo ufw allow 8552/tcp    # AuthRPC

# Ver estado del firewall
sudo ufw status verbose
```

> 💡 Si estás ejecutando otros clientes como Lighthouse o Grandine, también deberás permitir sus puertos correspondientes.

***

### 📝 Notas

* El firewall (UFW) puede estar bloqueando el tráfico por defecto, incluso si el nodo corre sin errores.
* Probar conectividad con `telnet`, `nc` o revisar logs puede ser útil.
* Siempre que se cambien puertos, verificar que **no haya conflicto con otros servicios** en el sistema.

***

¿Quién dijo miedo? Aquí seguimos debuggeando sin parar 🛠️⚡
