---
icon: hard-drive
---

# Cómo extender la partición LVM por defecto en Ubuntu 24.04

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt="" width="375"><figcaption><p><a href="https://es.wikipedia.org/wiki/Tumba_de_Liliana_Crociati_de_Szaszak">Tumba de Liliana Crociati de Szaszak</a></p></figcaption></figure>

Al instalar Ubuntu 24.04 en mi servidor recién ensamblado, me encontré con que el disco principal (`/`) estaba completamente lleno al 100%. Esto me sorprendió, ya que había instalado dos discos internos con amplio espacio de almacenamiento.

Al revisar, noté que la instalación por defecto crea una partición encriptada que utiliza **LVM** (Logical Volume Management). LVM es una forma de virtualizar el almacenamiento, permitiendo manejar volúmenes lógicos sobre dispositivos físicos reales. Esto significa que podemos redimensionar estos volúmenes según nuestras necesidades, mientras exista espacio disponible en el grupo de volúmenes (VG).

Por defecto, Ubuntu asigna solo **100 GB** al volumen lógico principal, pero este tamaño puede ampliarse fácilmente. A continuación te dejo los pasos que seguí, basados en este artículo:  [How to Extend the Default Ubuntu LVM Partition](https://packetpushers.net/blog/ubuntu-extend-your-default-lvm-space/), junto con comandos útiles y explicaciones.

***

### 1. 📈 Incrementar el tamaño del volumen de bloque

Primero, verifica el estado actual del disco:

```bash
$ df -h
```

Busca una línea similar a:

```
/dev/mapper/ubuntu--vg-ubuntu--lv   100G   100G   0  100% /
```

***

### 2. 🔎 Revisar el espacio disponible en el grupo de volúmenes (VG)

Para ver cuánto espacio libre queda en tu grupo de volúmenes (en este caso, `ubuntu-vg`):

```bash
$ vgdisplay
```

Busca la línea `Free PE / Size`, que indica el espacio libre que puedes asignar.

***

### 3. 📦 Verificar detalles del volumen lógico (LV)

Confirma que estás apuntando al volumen correcto:

```bash
$ lvdisplay
```

***

### 4. ➕ Extender el volumen lógico (LV)

Una vez identificado el nombre correcto del volumen lógico (por defecto `ubuntu-lv`), extiéndelo utilizando todo el espacio libre disponible en el grupo:

```bash
$ sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```

Verifica nuevamente:

```bash
$ lvdisplay
```

***

### 5. 🛠️ Redimensionar el sistema de archivos (`filesystem`)

Finalmente, expande el sistema de archivos para que aproveche el nuevo espacio:

```bash
$ sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

Verifica que el cambio se haya aplicado correctamente:

```bash
$ df -h
```

Deberías ver ahora una partición mucho más grande asignada a `/`.

***

<figure><img src="../.gitbook/assets/image (11).png" alt="" width="375"><figcaption><p>Recoleta Buenas Aires</p></figcaption></figure>

#### ✅ Resultado final esperado

Después de completar estos pasos, tendrás tu volumen lógico y sistema de archivos ampliado, utilizando todo el espacio disponible en tus discos físicos.
