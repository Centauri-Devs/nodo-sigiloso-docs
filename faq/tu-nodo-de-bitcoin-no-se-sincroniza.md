---
description: >-
  “Llevo semanas encendiendo el nodo, pero sigue atrasado… ¿qué estoy haciendo
  mal?”
---

# ¿Tu nodo de Bitcoin no se sincroniza?

***

### ⚙️ Estado actual

Tu nodo lleva **3 semanas corriendo**, pero solo ha alcanzado el **85% del progreso** de sincronización. Eso no está bien. Deberías estar más cerca del 100% en ese tiempo, especialmente si tu hardware no es muy viejo y tu red es estable.

```bash
bashCopyEditprogress=0.847138
```

***

### 🧭 Diagnóstico inicial

#### 🚫 ¿Problemas de red?

❌ Poco probable. Si otros nodos (como tus de Ethereum) sincronizan bien en la misma red, entonces no es tu conexión.

#### 💾 ¿Problemas de disco?

✅ **Estás usando un disco externo montado en** `/media/honey/bitcoin_data`:

```bash
bashCopyEdit/dev/sda        916G  680G  190G  79%
```

Parece un SSD de casi 1 TB. No hay errores de espacio, y el uso del 79% es aceptable.

**PERO**: Si es un SSD **viejo o sin TRIM activo**, puede ser **muy lento en operaciones de escritura aleatoria**, lo que **afecta directamente el rendimiento de Bitcoin Core**.

***

### 🔍 ¿Qué puedo revisar?

#### 1. Verifica el rendimiento del disco

Ejecuta esto para ver si es lento:

```bash
bashCopyEditsudo hdparm -Tt /dev/sda
```

Si da resultados por debajo de 100 MB/s (lectura), probablemente necesitas cambiar de disco o moverlo a un NVMe interno.

***

#### 2. Verifica cuántos peers tienes

```bash
bashCopyEditbitcoin-cli getnetworkinfo | grep connections
```

Si tienes menos de 8-10 conexiones, tu nodo se sincroniza lento.

Solución: abre más puertos o usa nodos públicos como bootstrap (por ejemplo: `addnode` en `bitcoin.conf`).

***

#### 3. Activa más caché de disco

Edita tu `bitcoin.conf` y añade:

```ini
iniCopyEditdbcache=2048
maxmempool=300
```

Y reinicia tu nodo. Esto puede **mejorar muchísimo** la velocidad de validación de bloques.

***

### 🌱 ¿Y si ya no quiero esperar?

Considera usar un "bootstrap" inicial descargando un snapshot verificado del blockchain (ej: [https://prunednode.today](https://prunednode.today)) y luego sincronizando desde ahí.

***

### ✍️ Reflexión final

> Correr un nodo no es solo prender una caja, es un **acto de soberanía tecnológica**.\
> Si se tarda... **no desesperes**, **optimiza**, **aprende** y sigue corriendo 🧸
