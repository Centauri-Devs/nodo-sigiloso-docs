---
icon: luchador-mask
---

# Ethereum: Consenso y Ejecución

### Ethereum: Consenso y Ejecución



Ethereum necesita correr dos tipos de clientes, o programas, que interactúan entre sí para correr aplicaciones descentralizadas. Cada uno de estos clientes tienen responsabilidades complementarias. Para que un nuevo bloque se agregue a la cadena de bloques, una mayoría de nodos tienen que llegar a consenzo.

En este momento, la cadena tiene 22442491 bloques en los que este grupo de nodos acuerdan, mediante un consenso, que se han cumplido las reglas por las que todos se rijen.

Grandine es un **cliente de consenso** de **código abierto**. Cada validador, para ser incluido dentro del set de validadores,  hacen staking de sus fondos dentro de la becon chain.

Si se desea utilizar el nodo como RPC, y no se quiere hacer staking, se puede correr y esperar a que se sincronice la cadena.

Existe tambien otro cliente de consenso, en rust y mucho mayor margen del mercado, Lighthouse🏮. Yo corro los dos.

Por el otro lado, hasta ahora somo hemos mencionado la parte oscura del consenso, también está la cadena número 1, por su chain id, Ethereum mainnet. Que, es donde están corriendo todos los contratos inteligentes y aplicaciones descentralizadas que utilizamos.

Para correr esas aplicaciones se utiliza el **cliente de ejecución**



### Ethereum: Consenso y Ejecución

Ethereum necesita ejecutar dos tipos de clientes, o programas, que interactúan entre sí para hacer funcionar las aplicaciones descentralizadas (dApps). Cada uno de estos clientes tiene responsabilidades complementarias: uno se encarga del **consenso**, y el otro de la **ejecución**.

Para que un nuevo bloque se agregue a la cadena, una mayoría de nodos debe llegar a un consenso. Actualmente, la cadena cuenta con **22,442,491 bloques**, todos acordados bajo las reglas comunes a las que se adhieren los participantes de la red.

#### Cliente de consenso

Uno de los clientes de consenso que utilizo es **Grandine**, un cliente de código abierto. Cada validador, para ser incluido dentro del conjunto activo, debe hacer _staking_ de 32 ETH en la _Beacon Chain_.

Si solo se desea usar el nodo como proveedor de datos (_RPC node_) sin participar en el staking, también es posible: simplemente se corre el nodo y se espera a que se sincronice con la red.

Otro cliente de consenso muy popular, escrito en Rust, es **Lighthouse 🏮**, que tiene una mayor cuota de mercado. Yo corro ambos: Grandine y Lighthouse, para experimentar y comparar su comportamiento.

#### Cliente de ejecución

Hasta ahora hemos hablado únicamente del consenso —la parte “oscura” y silenciosa del proceso. Pero también está la capa de ejecución, a menudo identificada como **Ethereum Mainnet (Chain ID: 1)**. Aquí es donde realmente viven y se ejecutan los contratos inteligentes y las aplicaciones descentralizadas que usamos todos los días.

Para correr estas aplicaciones, se necesita un **cliente de ejecución**, que interactúe con la cadena y ejecute el código de los contratos.

La capa de ejecución es donde ocurren las interacciones visibles de Ethereum: contratos inteligentes, tokens, aplicaciones DeFi, NFTs, DAOs y más. Para que todo esto funcione, se necesita un **cliente de ejecución** que reciba transacciones, las valide y ejecute el código de los contratos según las reglas del protocolo.

El cliente de ejecución más utilizado históricamente es **Geth (Go-Ethereum)**, desarrollado en Go por la Fundación Ethereum. Es el cliente más maduro y compatible, y ha sido durante años el estándar de facto para desarrolladores y operadores de nodos.

Sin embargo, en tiempos más recientes ha ganado mucha tracción **Reth**, un cliente de ejecución escrito en **Rust**, desarrollado por el equipo de Paradigm. Reth ha sido diseñado desde cero con un enfoque en seguridad, modularidad y rendimiento, aprovechando todo el poder y las garantías del lenguaje Rust.

Yo personalmente utilizo Reth, no solo porque está escrito en un lenguaje que me apasiona, sino porque ofrece tiempos de sincronización más rápidos, menor uso de recursos y una arquitectura limpia que facilita su integración en sistemas más complejos.

Además de Geth y Reth, existen otros clientes de ejecución como:

* **Erigon**, enfocado en archivado y eficiencia en almacenamiento.
* **Besu**, ideal para entornos empresariales y compatibles con redes privadas.
* **Nethermind**, escrito en C# y muy usado en algunos entornos de investigación.

Cada cliente tiene sus particularidades, pero todos cumplen el mismo propósito: ejecutar la Ethereum Virtual Machine (EVM) y mantener el estado de la red.
