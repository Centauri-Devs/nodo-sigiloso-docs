---
icon: block-brick-fire
---

# UFW

sudo ufw status



### 🔗 Network Configuration <a href="#network-configuration" id="network-configuration"></a>

The standard UFW - Uncomplicated firewall can be used to control network access to your node and protect against unwelcome intruders.

#### Configure UFW Defaults <a href="#configure-ufw-defaults" id="configure-ufw-defaults"></a>

By default, deny all incoming traffic and allow outgoing traffic.

```
6  sudo ufw default deny incoming
7  sudo ufw default allow outgoing

Configure SSH Port 22
8  sudo ufw allow from 177.177.1.0/24 to any port 22 proto tcp comment 'Allow SSH from local network'

Execution
9  sudo ufw allow 30303 comment 'Allow execution client port'
```



Consensus

10 sudo ufw allow 9000 comment 'Allow consensus client port'\
11 sudo ufw enable\
12 sudo ufw status numbered\
13 history

177.177.1.0 <- local network.

ludo ufw allow from 177.177.1.0/24 to any port 22 proto tcp comment 'Allow SSH from local network'

por favor visitar: [https://www.coincashew.com/spanish/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet/part-i-installation/step-2-configuring-node](https://www.coincashew.com/spanish/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet/part-i-installation/step-2-configuring-node)
