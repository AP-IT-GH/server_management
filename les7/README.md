# Les 7: DHCP

Het **Dynamic Host Configuration Protocol** stelt on in staat om het management
van de ip configuratie te centraliseren. Door de configuratie op een plaats te
voorzien verminderen we de kans op fouten. DHCP configureert ook meer dan
alleen maar een ip. Het configureert ook de volgende items:
* Subnetmask
* Broadcast Address
* Default Gateway / Router
* DNS Server


Het is ook mogelijk het domain naam te verdelen en hostnames maar dit is buiten
de scope van het labo.


## Client Configuratie
Om een adres van de dhcp server te verkrijgen moeten er geen extra software
worden voorzien, deze staat default geïnstalleerd. Er moet wel gezien worden
dat de netwerk kaart geconfigureerd staat om een IP te verkrijgen via DHCP.

Dit wordt mogelijk ingesteld in de file `/etc/network/interfaces`

*Netwerkkaart configuratie voor DHCP*

```
auto eth0
iface eth0 inet dhcp
```

Op een Windows systeem kan het volgende commando gebruikt worden om een DHCP
adres te krijgen en/of te vernieuwen.

`ipconfig /renew`

Op een linux systeem gebeurt dit met het volgende commando.

`sudo dhclient -r [INTERFACE]`

## Server Configuratie

Als DNS software gebruiken we het volgende pakket:

`isc-dhcp-server`

De configuratie staat zo als altijd in de `/etc` folder het volledige path van de configuratie file is `/etc/dhcp/dhcpd.conf`


De configuratie file kunnen we in 3 grote delen opdelen:
1. Global Options
2. Subnet Definitions
3. Static Host Definitions

### Global options Options

|Optie Naam         |Beschrijving               |
|--                 |--                         |
|default-lease-time |De lease time die wordt meegegeven vanuit de DHCP server, dit is de tijd dat het adres voor een specifieke client gereserveerd blijft. |    
|max-lease-time     |De lease time kan door de client worden overschreven t/m de max-lease-time                                                             |
|subnet-mask        |De subnet-mask van een subnet dat wordt meegegeven aan de client                                                                       |
|broadcast-address  |Het broadcast-address voor het subnet, dit moet verwijzen naar het hoogste adres in de subnet range                                    |
|routers            |Een dubbelzinnige naam, met deze optie wordt de default gateway voorzien                                                               |
|domain-name-server |Hiermee wordt de DNS server ingesteld                                                                                                  |

### Subnet Configuratie

Het is mogelijke om af te wijken van de globale opties in de config file, dit
zal voor het labo niet nodig zijn want er wordt maar 1 netwerk gedefinieerd. 
Het enigste wat er gedefineerd moet worden is de range die wordt verdeeld aan
mogelijke clients. Deze range kan afwijken van het maximale beschikbare ip
adressen in het subnet.


*Een mogelijke configuratie*
```
subnet 123.145.167.0 netmask 255.255.255.0 {
   range 123.145.167.33 123.145.167.66
}
```

### Static Host Configuratie
Het is mogelijk om een host altijd hetzelfde ip adres toe te wijzen. Dit wordt
meestal gebruikt voor het distribueren van IP adressen aan servers. Deze
toewijzing gebeurt aan de hand van MAC adressen. MAC adressen zijn gebonden aan
de hardware en is zijn zeer moeilijk om te veranderen. De configuratie voor een
statisch IP adres ziet er als volgt uit:

*statisch IP configuratie*

```
host websrv {
   hardware ethernet 06:05:2c:45:5d:2e;
   fixed-address 123.145.167.22;
}
```

### Toewijzen aan een interface

De laatste configuratie die nog moet gebeuren is het toewijzen van de DHCP
server aan een interface. Door deze toewijzing zal de DHCP server alleen maar
IP adressen uitdelen via de specifieke interface.

Deze toewijzing gebeurt in de file `/etc/default/isc-dhcp-server`.

In de files in `/etc/default`  worden de opstart parameters gedefinieerd. Dit
kan vergelijken worden met de parameters die worden meegegeven aan een
commando. 

In de file `/etc/default/isc-dhcp-server` moet de `INTERFACES` variabele worden
aangepast naar de correcte interface.  

*INTERFACES aanpassing*

`INTERFACES="eth1"

## Links / Tutorials
* http://www.tldp.org/HOWTO/DHCP/x369.html
* https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-dhcp-configuring-server.html
* https://help.ubuntu.com/community/isc-dhcp-server
