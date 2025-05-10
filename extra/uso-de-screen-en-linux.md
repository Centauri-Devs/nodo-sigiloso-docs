---
icon: server
---

# Uso de screen en Linux

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="375"><figcaption><p>Gracias Linux</p></figcaption></figure>

Tengo mi servidor pequeno, y para permitirle correr multiples trabajos al mismo tiempo. O lo que viene siendo lo mismo, dejar corriendo algo. Se utiliza el comando de Linux screen.

## Instalar el comando screen

```bash
$ sudo apt install screen
```

## Abrir una nueva ventana y dejarla correr

```bash
$ screen -ls

$ screen -S machine-gun

# On the Keyboard cmd + A + D to detach screen

$ screen -r machine-gune # to jump into screen
```

