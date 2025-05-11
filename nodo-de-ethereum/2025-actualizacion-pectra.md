---
icon: hammer-crash
---

# 2025 Actualización Pectra

### ¿Cuándo se lanza _Pectra_ en Ethereum?

**Pectra** (la fusión de **Prague + Electra**) es la próxima gran actualización de Ethereum.\
Según los desarrolladores de Ethereum, **la fecha estimada para Pectra en mainnet es en el tercer o cuarto trimestre de 2025**, aunque **no hay una fecha oficial confirmada aún**.

***

### ✨ ¿Qué cambia con Pectra para los validadores?

Uno de los cambios más esperados es:

#### 🔐 Las credenciales de retiro tipo `0x02`

* Las credenciales de tipo `0x01` envían automáticamente las recompensas al _withdrawal address_ en L1 (por ejemplo, una dirección `0x...` de Ethereum).
* Las credenciales de tipo `0x02` permiten que **el validador retire y vuelva a depositar más ETH**, **más allá del límite original de 32 ETH**.

Esto significa que, **una vez que Pectra esté en vivo**, si tu validador usa credenciales `0x02`, podrás:

* Seguir acumulando recompensas en el _balance efectivo_ de tu validador
* Aumentar el stake más allá de los 32 ETH iniciales

***

#### 🛡️ Pectra y el Futuro de los Validadores en Ethereum

**Pectra** es el nombre clave de una actualización que unifica los desarrollos de **Prague** (en capa de ejecución) y **Electra** (en capa de consenso).\
Está planeada para activarse en **mainnet durante la segunda mitad de 2025**.

Uno de los cambios más importantes es la introducción de las **credenciales de retiro `0x02`**.

> ✨ Estas credenciales permiten que un validador incremente su stake **más allá de los 32 ETH originales**, algo que antes no era posible.

**¿Qué tipo de credencial tengo?**

* Si tu credencial de retiro es `0x01`: tus recompensas se retiran automáticamente a tu dirección L1.
* Si tu credencial de retiro es `0x02`: **podrás incrementar tu stake** una vez que la actualización de Pectra esté activa.

**¿Qué necesito hacer?**

Si ya estás operando un nodo validador con credenciales `0x01`, **no podrás migrar a `0x02`**.\
Para aprovechar esta funcionalidad, deberás generar una nueva clave de retiro tipo `0x02` y realizar un nuevo depósito de validación.
