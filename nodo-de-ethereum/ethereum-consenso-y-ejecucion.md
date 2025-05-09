---
description: Introducción a los dos clientes que permiten la ejecución de Ethereum.
icon: luchador-mask
---

# Ethereum: Consenso y Ejecución

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption><p>Consenso entre los nodos de Ethereum</p></figcaption></figure>

Ethereum necesita ejecutar dos tipos de clientes, o programas, que interactúan entre sí para hacer funcionar las aplicaciones descentralizadas (dApps). Cada uno de estos clientes tiene responsabilidades complementarias: uno se encarga del **consenso**, y el otro de la **ejecución**.

Para que un nuevo bloque se agregue a la cadena, una mayoría de nodos debe llegar a un consenso. En este momento, la cadena cuenta con **22,442,491 bloques**, todos acordados bajo las reglas comunes a las que se adhieren los participantes de la red.

### 🌞 Cliente de consenso

Uno de los clientes de consenso que utilizo es **Grandine**, un cliente de código abierto. Cada validador, para ser incluido dentro del conjunto activo, debe hacer _staking_ de, al menos, 32 ETH en la _Beacon Chain_. Porque con la nueva actualización de Pectra, los nodos podrán manejar una cantidad mayor.

Si solo se desea usar el nodo como proveedor de datos (_RPC node_) sin participar en el staking, también es posible: simplemente se corre el nodo y se espera a que se sincronice con la red.

Otro cliente de consenso muy popular, escrito en Rust, es **Lighthouse 🏮**, que tiene una mayor cuota de mercado. Yo corro ambos: Grandine y Lighthouse, para experimentar y comparar su comportamiento.

### ⚙️ Cliente de ejecución

Hasta ahora hemos hablado únicamente del consenso —la parte “oscura” y silenciosa del proceso. Pero también está la capa de ejecución, a menudo identificada como **Ethereum Mainnet (Chain ID: 1)**. Aquí es donde realmente viven y se ejecutan los contratos inteligentes y las aplicaciones descentralizadas que usamos todos los días.

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="375"><figcaption><p>Conociendo al cliente de ejecución</p></figcaption></figure>

Para correr estas aplicaciones, se necesita un **cliente de ejecución**, que interactúe con la cadena y ejecute el código de los contratos.

La capa de ejecución es donde ocurren las interacciones visibles de Ethereum: contratos inteligentes, tokens, aplicaciones DeFi, NFTs, DAOs y más. Para que todo esto funcione, se necesita un **cliente de ejecución** que reciba transacciones, las valide y ejecute el código de los contratos según las reglas del protocolo.

El más utilizado históricamente es **Geth (Go-Ethereum)**, desarrollado en Go por la Fundación Ethereum. Es el cliente más maduro y compatible, y ha sido durante años el estándar de facto para desarrolladores y operadores de nodos.

Sin embargo, en tiempos más recientes ha ganado mucha tracción **Reth**, un cliente de ejecución escrito en **Rust**, desarrollado por el equipo de Paradigm. Reth ha sido diseñado desde cero con un enfoque en seguridad, modularidad y rendimiento, aprovechando todo el poder y las garantías del lenguaje Rust.

Además de Geth y Reth, existen otros clientes de ejecución como:

* **Erigon**, enfocado en archivado y eficiencia en almacenamiento.
* **Besu**, ideal para entornos empresariales y compatibles con redes privadas.
* **Nethermind**, escrito en C# y muy usado en algunos entornos de investigación.

Cada cliente tiene sus particularidades, pero todos cumplen el mismo propósito: ejecutar la Ethereum Virtual Machine (EVM) y mantener el estado de la red.
