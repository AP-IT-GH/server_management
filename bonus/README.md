# Bonus Opdracht: SSH Jump Server
Volgende opdracht mag ingediend worden voor extra bonuspunten. Dez opdracht is
niet verplicht. Deze opdracht is een oefening voor het opzetten van netwerken
in VirtualBox.

Het doel van dit labo is om een ssh jump server te configureren.

## Netwerk Diagram

```
+--------------+              +--------------+             +--------------+
|              |              |              |             |              |
|              +-+          +-+              +-+         +-+              |
|   Host       |1+----------+2|   Server 1   |3+---------+4|   Server 2   |
|              +-+          +-+              +-+         +-+              |
|              |              |              |             |              |
+--------------+              +--------------+             +--------------+
```

***Legende:***

1. Ethernet Interface op HostOnly Network #3 
2. Ethernet Interface attached to HostOnly Network #3 
3. Ethernet Interface attached to Internal Network #1 
4. Ethernet Interface attached to Internal Network #1 

> NOOT: Alle servers hebben ook nog een bridged adapter.

## IP Configuratie

1. 192.168.111.MM
2. 192.168.111.MM+1
3. 192.168.222.DD
4. 192.168.222.DD+1

> Waarbij DD geboortedag is en MM geboortemaand.
> Alle IP worden statisch ingesteld.

## Server Software 
 * Server 1:
    * openssh-server
 * Server 2:
    * openssh-server
> Er is geen speciale configuratie nodig.

## Users
* Server 1:
    * achternaam (luyts)
* Server 2:
    * voornaam (maarten)

> Voor alle users wordt een homedirectory aangemaakt.


**Dit is de configuratie van het labo. De vereiste van het verslag staan in labo.md** 
