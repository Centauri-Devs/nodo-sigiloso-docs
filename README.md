---
icon: hand-wave
cover: .gitbook/assets/c88c19c9-2337-4df3-b6e3-5ed7c5aabd66.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Welcome

<figure><img src=".gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption><p>Teatro Morelos Morelia, Michoacán</p></figcaption></figure>

Bienvenid@ a la documentación oficial de **Nodo Sigiloso**, tu compañero discreto para operar infraestructura blockchain y construir exploradores multicadena.

Tanto si eres operador de nodos, desarrollador curioso o simplemente quieres consultar datos de blockchains sin depender de terceros… este proyecto es para ti.

## 🚀 ¿Qué es Nodo Sigiloso?

Nodo Sigiloso es una iniciativa abierta para ayudarte a desplegar y mantener nodos blockchain de forma segura, económica y soberana.

Ofrecemos:

* 🧱 Guías para montar tu propia infraestructura: nodos de Bitcoin, Ethereum (L2s) y NEAR, con indexadores opcionales.
* 🔍 Una API llamada Explorador para consultar datos blockchain en tiempo real, ya sea desde tus propios nodos o desde nuestros endpoints públicos.

**Nuestra misión**: hacer que operar nodos sea algo accesible, elegante y enfocado en la privacidad — para los builders, por los builders.

## 📚 Estructura de la documentación

La documentación está dividida en dos secciones principales:

### 1. 🛠 Corre tu propia infraestructura

Pasos para instalar y operar nodos completos o indexadores de:

* Bitcoin — Nodo completo o podado
* Ethereum / L2s — Incluye indexadores personalizados y proveedores RPC
* NEAR Protocol — Con configuración para validadores

Cada guía incluye recomendaciones de hardware, configuración con Docker, sincronización y monitoreo.

### 2. 🔎 Explorador Sigiloso API

La explorador\_sigiloso\_api es un backend multi-cadena que te permite:

Ver actividad por dirección BTC

Consultar deltas de bloques (entradas, salidas, recompensas)

Acceder a estadísticas on-chain personalizadas

Ideal para crear dashboards, alertas, bots o alimentar tus propias apps — todo esto usando tus propios nodos o los nuestros.

🧭 Primeros pasos

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Infraestructura</strong></td><td>Guía para correr nodos BTC, ETH y NEAR</td><td></td><td></td><td><a href="infra/overview.md">overview.md</a></td></tr><tr><td><strong>API Explorador</strong></td><td>Consulta datos en tiempo real</td><td></td><td></td><td><a href="api/intro.md">intro.md</a></td></tr><tr><td><strong>Despliegue con Docker</strong></td><td>Corre todo local o en servidor</td><td></td><td></td><td><a href="deploy/docker.md">docker.md</a></td></tr></tbody></table>

🧪 Esta documentación está en desarrollo activo — se irá actualizando semanalmente mientras mejoramos el explorador, la API y los manuales de despliegue.

¿Quieres contribuir o dejar tu estrella? Visita el repo:\
👉 github.com/josemariasosa/explorador-sigiloso
