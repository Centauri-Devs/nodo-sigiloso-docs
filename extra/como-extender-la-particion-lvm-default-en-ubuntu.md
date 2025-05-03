---
icon: hard-drive
---

# Cómo extender la partición LVM default en Ubuntu

Al momento de instalar Ubuntu 24 en el servidor que acababa de ensamblar e instalar Rust y Docker, vi que mi disco principal, `/` , estaba completamente lleno al 100%. Esto me resultó muy raro, puesto que había instalado dos discos duros internos de un gran almacenamiento.

Además, la partición principal del disco se encuentra encriptada y utiliza LVM, Logical volume management (LVM) is a form of storage virtualization, que significa memoria virtual. Esto entonces quiere decir que hay dos memorias, la real y la virtual. Y la virtual se puede ajustar para adecuarse a las necesidades del servidor, teniendo el espacio físico de almacenamiento real como límite.

La instalación, por default asigna 100GB de almacenamiento, pero este se puede incrementar. Para hacerlo encontré el siguiente artículo: [How to Extend the Default Ubuntu LVM Partition](https://packetpushers.net/blog/ubuntu-extend-your-default-lvm-space/). Acá un resúmen de los comandos.

### 1. Incrementar el tamaño del volumen de bloque

Para incrementar el espacio de almacenamiento virtual, hay que asegurarse de que la memoria actual está siendo utilizada.

```bash
$ df -h

# TODO: Resultado
/dev/mapper/ubuntu--vg-ubuntu--lv
```

Para revisar el espacio libre existente en nuestro Volume Group (VG).

```bash
$ vgdisplay
# TODO: Resultado
```

Para utilzar ese espacio libre en el Volume Group (VG) dentro de nuestro Logical Volumen (LV).

```bash
$ lvdisplay
# TODO: Resultado

$ lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv

# Correr de nuevo, para asegurarse que se aplicó el cambio
$ lvdisplay
# TODO: Resultado
```

### 2. Extender el \`filesystem\`

Revisar el uso de los discos y extender el \`filesystem\`.

```bash
$ df -h

$ resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv

$ df -h
```
