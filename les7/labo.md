# Labo: DHCP

Voor dit labo zullen gebruik maken van meerdere virtuele machines. In een
VirtualBox host-only netwerk, zal een DHCP server geplaatst worden die de een
IP zal voorzien voor verschillende clients. Deze clients kunnen een
verschillende rol hebben, hierdoor zullen afhankelijk van deze rol een statisch
of dynamisch IP adres worden toegewezen.

## Beschrijving virtuele machines
In dit gedeeltde worden de virtuele machines beschrijven afhankelijk van hun netwerk noden.

* DHCP Server (Ubuntu Server)
  * 1 NIC Attached to: Bridged
  * 1 NIC Attached to: Host-Only Network #2
* DHCP Client Static (Ubuntu Server)
  * 1 NIC Attached to: Host-Only Network #2
* DHCP Client Dynamic (Ubuntu Server)
  * 1 NIC Attached to: Host-Only Network #2

```
                         WWW
                          ^
                          |
                          |
+-----------------------------------------------------+
|                         |                           |
|                   +-----+------+                    |
|                   |            |                    |
|                   |    DHCP    |                    |
|            +------+   SERVER   +------+             |
|            |      |            |      |             |
|            |      |            |      |             |
|            |      |            |      |             |
|            |      +------------+      |             |
|            |                          |             |
|            |                          |             |
|            |                          |             |
|      +-----v------+            +------v-----+       |
|      |            |            |            |       |
|      |    DHCP    |            |    DHCP    |       |
|      |   CLIENT   |            |   CLIENT   |       |
|      |            |            |            |       |
|      |  DYNAMIC   |            |   STATIC   |       |
|      |            |            |            |       |
|      +------------+            +------------+       |
|                                                     |
|                                                     |
|                                                     |
+-----------VirtualBox Host Only Network-#2+----------+
```

## Opdracht

* Installeer de DHCP server software
* Gebruik het volgende netwerk:  
    * Subnet: `DD.MM.YY.0/24` *Waarbij `DD.MM.YY` je eigen geboorte datum is.*
    * DNS Server: `8.8.8.8` (Google Public DNS).
    * Default Gateway / router:  `DD.MM.YY.1`

* De DHCP deelt alleen maar IP uit langs de host-only interface.
* Configueer de host-only interface van de DHCP server met het IP `DD.MM.YY.127`.
* Geef de statische client het volgende IP adres vanuit de DHCP server `DD.MM.YY.126`.
* Reserveer een IP range voor dynamische clients van `128` tot `254`.

## Verslag 

* dhcpd.conf file
* output van tracepath vanuit de dynamische DHCP client.
