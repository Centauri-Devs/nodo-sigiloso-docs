---
description: >-
  Las palabras mnemómincas nos ayudan a generar llaves privadas para cualquier ,
  o al menos un número muy grande, de blockchains.
---

# Las palabras son una semilla

Aqui comienza...



```
      +----------------------+
      |  12–24 palabras      |
      |  (frase mnemónica)   |          BIP 39 
      +----------------------+
                |
                v
      +----------------------+
      |       Semilla        |
      |  (512 bits típico)   |
      +----------------------+
                |
                v
      +----------------------+
      |  Cadena (master key) |
      |  y datos de cadena   |
      +----------------------+
                |
                v
      +----------------------+
      |      Encoding        |
      | • Hexadecimal        |
      | • Base58Check        |
      | • Bech32             |
      +----------------------+

```

<figure><img src=".gitbook/assets/image.png" alt="" width="375"><figcaption></figcaption></figure>
