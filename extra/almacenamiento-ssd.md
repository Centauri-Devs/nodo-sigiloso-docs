---
icon: floppy-disk
---

# Almacenamiento SSD

### 1. Listar los discos disponibles

Para localizar el disco, físico o virtual, en el que se va a trabajar, se puede utilizar el comando **lsblk**.

```bash
$ lsblk

NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda           8:0    0 931.5G  0 disk /media/honey/bitcoin_data
mmcblk0     179:0    0  59.6G  0 disk
|-mmcblk0p1 179:1    0   512M  0 part /boot/firmware
`-mmcblk0p2 179:2    0  59.1G  0 part /
```

En Mac, se puede utilizar **diskutil list**.

```bash
$ diskutil list

/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.3 GB   disk0
   1:             Apple_APFS_ISC Container disk1         524.3 MB   disk0s1
   2:                 Apple_APFS Container disk3         494.4 GB   disk0s2
   3:        Apple_APFS_Recovery Container disk2         5.4 GB     disk0s3

/dev/disk3 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +494.4 GB   disk3
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD            11.2 GB    disk3s1
   2:              APFS Snapshot com.apple.os.update-... 11.2 GB    disk3s1s1
   3:                APFS Volume Preboot                 7.2 GB     disk3s2
   4:                APFS Volume Recovery                1.0 GB     disk3s3
   5:                APFS Volume Data                    404.8 GB   disk3s5
   6:                APFS Volume VM                      5.4 GB     disk3s6
```

### 2. Espacio disponible y utilizado

Antes de comenzar, asegúrate de que tienes un SSD montado con suficiente espacio libre. Esto es crítico para correr un nodo Bitcoin confiable.

```bash
# Verifica el espacio disponible
$ df -h /media/honey/bitcoin_data/

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda        916G  360G  510G  42% /media/honey/bitcoin_data
```

### 3. Montaje y desmontaje del SSD

```bash
# Montar
sudo mkdir -p /mnt/bitcoin-data
sudo mount /dev/sda /mnt/bitcoin-data

# Desmontar
sudo umount /mnt/bitcoin-data
```
