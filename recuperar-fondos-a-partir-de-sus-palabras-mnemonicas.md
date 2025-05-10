---
description: >-
  Guía paso a paso para recuperar una cartera digital a partir de las 12 - 24
  palabras mnemónicas.
icon: acorn
---

# Recuperar fondos a partir de sus palabras mnemónicas

Lo primero es recordar, cómo fue que se crearon las llaves de aquella cartera. Fue mediante una billetera externa, o tirando dados 🎲.

***

<figure><img src=".gitbook/assets/image (5).png" alt="" width="375"><figcaption></figcaption></figure>

## La ardilla resurge: Origen y recuperación de tu semilla

**Antes de restaurar una cartera**, recuerda cómo se generaron tus claves:

* **Wallet externo o hardware**: la aplicación proporcionó tu frase mnemónica BIP39.
* **Método manual**: entropía generada con dados 🎲.

_Consulta con tu proveedor de wallet el procedimiento exacto de backup y restore que emplea._

***

### 1. Estándares de semilla: BIP39 vs SLIP39

**BIP39 (mnemónico clásico)**

* Frase de 12–24 palabras de un vocabulario de 2 048 términos.
* Cada palabra codifica 11 bits; ENT + CS bits → semilla de 512 bits.

**SLIP39 (Shamir Seed Sharing)**

1. Elige un umbral _t_ y un total de _n_ fragmentos (shares).
2. Convierte la semilla maestra en la constante de un polinomio de grado _t – 1_ sobre un campo finito.
3. Evalúa el polinomio en _n_ puntos distintos → _n_ fragmen­tos.
4. Cualquier conjunto de _t_ fragments permite interpolar el polinomio y **reconstruir la semilla**; con menos de _t_ no hay información.

_Ideal para repartir confianza sin exponer todo el secreto._

***

### 2. Derivación de claves: BIP44

Tras generar la semilla (BIP39 o SLIP39), aplica la ruta jerárquica BIP44:

```
m/44'/<moneda>'/<cuenta>'/0/0
```

* `<moneda>`: 0 (Bitcoin), 60 (Ethereum), 397 (NEAR)
* `<cuenta>`: índice de cuenta (normalmente 0)

Esto deriva tu clave maestra extendida (xprv/xpub) y de ahí salen todas tus direcciones.

***

### 3. Cuatro pasos para restaurar tu monedero

Cuando el reloj corre y cada bit vale, sigue estos pasos:

1. **Entorno seguro**
   * Dispositivo limpio y actualizado.
   * Red confiable (evita Wi‑Fi públicas).
   * Mnemónico BIP39 o fragmentos SLIP39 alineados.
2. **Elegir la wallet**
   * **Multicadena**: Exodus, Atomic, Trust Wallet.
   * **Especializada**:
     * BTC → Electrum
     * ETH → MetaMask / MyEtherWallet
     * NEAR → NEAR Wallet / `near-cli`
   * Debe soportar “Restore from seed” o “Shamir shares”.
3. **Importar y derivar**
   * Selecciona “Importar cuenta” o “Restore from seed”.
   * Ingresa tu frase o tus _t_ fragmentos Shamir.
   * Si pide passphrase BIP39, déjala vacía salvo que la usaras.
   * Confirma la ruta BIP44 por defecto.
4. **Verificar y reforzar**
   * Espera sincronización y escaneo de direcciones.
   * Comprueba saldos en BTC, ETH y NEAR.
   * Refuerza seguridad: contraseña fuerte, respaldo físico y 2FA/PIN.

***

_Con estos pasos, tu “ardilla” recupera la semilla y protege tu bosque de fondos._















Busca a tu proveedor de wallet y pregúntale sobre el procedimiento en particular para reestablecer una cartera.

El estandar de las palabras mnemónicas en Bitcoin proviene del bip39, sin embargo en la actuallidad ya existen otras alternativas como el SLIP39, el cual utiliza un procedimiento conocido como shamir seed sharing.

A question for you mister machine, Can you explain how the shamir thing works, and sort everything again, including the 4 steps.\
\
The steps are good, but I would like to give a broad explanation that how thinks work, my fellow mexican engineers are amazing, so lets dive on the importants.\
\
Then after the seed is generated either bip39 or slip39, then after the same bip44 runs right, it is a question?\
\


#### 1. Preparar un entorno seguro

* Elige un dispositivo limpio y actualizado.
* Conéctate a una red fiable (evita Wi-Fi públicas).
* Ten a mano tu frase de 12–24 palabras, correcta y en orden.

#### 2. Seleccionar la wallet adecuada

* **Multicadena**: Exodus, Atomic Wallet, o Trust Wallet.
* **Especializada**:
  * Bitcoin: Electrum (BIP39/BIP44).
  * Ethereum: MetaMask o MyEtherWallet.
  * NEAR: NEAR Wallet (web) o `near-cli`.
* Comprueba que la wallet permita restaurar por “Seed phrase” o “Recovery phrase”.

#### 3. Importar la frase y configurar derivación

* Abre la opción **“Importar cuenta”** / **“Restore from seed”**.
* Introduce tu frase mnemónica palabra por palabra.
* Si se solicita passphrase adicional (BIP39), déjala en blanco salvo que la usaras.
*   Selecciona la ruta de derivación por defecto (BIP44):

    ```
    m/44'/<moneda>'/<cuenta>'/0/0
    ```

    * Bitcoin → `<moneda>` = 0
    * Ethereum → `<moneda>` = 60
    * NEAR → `<moneda>` = 397

#### 4. Verificar saldos y reforzar seguridad

* Espera a que la wallet sincronice y escanee direcciones.
* Confirma que tus fondos aparecen en cada red (BTC, ETH, NEAR).
* Refuerza la protección:
  * Establece contraseña fuerte.
  * Guarda la frase en un soporte físico seguro.
  * Habilita 2FA o PIN si la wallet lo permite.
