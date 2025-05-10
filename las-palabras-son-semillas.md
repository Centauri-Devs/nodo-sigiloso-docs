---
description: >-
  Las palabras mnemómincas nos ayudan a generar llaves privadas para cualquier ,
  o al menos un número muy grande, de blockchains.
---

# Las palabras son semillas

<figure><img src=".gitbook/assets/image (2) (1).png" alt="" width="375"><figcaption></figcaption></figure>

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

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Una vision alternativa.

<figure><img src=".gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

aca sigue\
\
Las mnemónicas provienen de BIP39:\
• BIP39 define cómo convertir una lista de 12–24 palabras en una semilla de alta entropía.\
• Cada palabra se serializa a una cadena de 11 bits (0–2047).\
• Se concatenan ENT (128–256 bits) + CS (checksum) bits para formar el total de bits.

```
 +----------------------+
 |      BIP39           |
 +----------------------+
           |
           v
 +----------------------+
 | 12–24 palabras       |
 | (frase mnemónica)    |
 +----------------------+
           |
           v
 +----------------------+
 |  Bits (ENT + CS)     |
 +----------------------+
           |
           v
 +----------------------+
 |     Semilla (512b)   |
 +----------------------+
           |
           v
 +----------------------+
 | Cadena maestra (xprv)|
 | y datos de cadena    |
 +----------------------+
           |
           v
 +-------------------------------------------+
 | Ruta de derivación (BIP44)                |
 | m / propósito' / tipo_moneda' / cuenta'   |
 |     / cambio / índice_dirección           |
 +-------------------------------------------+
 Ejemplo: m/44'/0'/0'/0/0
```

BIP44 define la estructura de rutas:

1. propósito: 44' (hardened)
2. tipo\_moneda: 0' para Bitcoin, 60' para Ethereum…
3. cuenta: índice de cuenta (normalmente 0')
4. cambio: 0 para externo, 1 para interno
5. índice\_dirección: 0, 1, 2, …

Con esto, cada nodo puede derivar claves privadas y públicas de forma determinista y jerárquica.
