# Les 6: DNS
Het **Domain Name Systeem** voorziet een translatie van een IP naar een domain
name, een vertaling van cijfers naar een lettercombinatie. Het is de
"telefoonboek van het internet".

DNS in het publieke domein wordt gemanagemed door de root servers. Deze werking
van deze servers is buiten de scope van dit labo. Voor het labo zal er een DNS
server worden opgesteld zoals het gebruikt kan worden in een development
omgeving. Het is mogelijk dat er een in een lokaal netwerk, een DNS server
wordt opgesteld. Dit wordt gedaan om de verschillende servers in een
development omgeving makkelijk te kunnnen bereiken en verplaatsbaar te maken.

## Hosts 

Op elk linux machine bevind zich op `/etc/hosts` file. Deze file is een
statische lookup table for hotsnames. Hierdoor kan snel een ip adres koppelen
aan een naam zonder een volwaardige DNS server te moeten instellen. Hier staat
standaard ook de `localhost` entry in.

Meer informatie staat in de man page `man hosts`.


*Voorbeeld hosts file*
```
# /etc/hosts: static lookup table for host name

#<ip-address>   <hostname.domain.org>   <hostname>
127.0.0.1   localhost.localdomain   localhost
::1     localhost.localdomain   localhost
192.168.0.149   rpi         rpi

# End of file
```

## resolv.conf

Om te zien welke DNS server er is ingesteld gebruik je het volgende commando
`/etc/resolv.conf`. Deze file wordt gegenereerd door resolvconf. De
implementatie van resolvconf verschild van de default resolvconf implementate.

## bind9 

*bind9* is een van de meeste gebruikte DNS server toepassingen. In een lokale
omgeving kan bind9 voor 2 doeleinden worden ingesteld.

1.  Caching DNS server  
    De caching DNS server zorgt ervoor dat er verder gezocht wordt als op het
    lokale machine geen dns entry is voor een query. Als er een match gevonden
    is, wordt er lokaal een kopie opgeslagen.

2.  Master DNS zone server  
    Een DNS zone server voorziet de ip adressen voor een domein. Je kan dus de
    records voorzien voor een eigen domein.

De configuratie files voor *bind9* staan in `/etc/bind` 

| File                                  | Doel                                  |
| --                                    | --                                    |
| /etc/bind/named.conf                  | Hoofd configuratie file wijst naar die file die mee worden ingeladen bij het opstarten van bind9                                      |
| /etc/bind/named.conf.options          | Zet de algemene bind opties                                      |
| /etc/bind/named.conf.default-zones    | Hierin staat de verwijzing naar de DNS zones die bij elke installatie van bind9 mee worden geinstalleerd.
| /etc/bind/named.conf.local            | De lokale DNS zones worden hier in gedefineerd.                                      |

### Caching DNS Server

De caching DNS server is een optie die we moeten aanzetten. Er zijn
verschillende DNS servers opties, die als forward DNS server kunnen gebruikt
worden bv: 
* ISP DNS
* Google Public DNS

Dit is een optie, de forwarders zijn daardoor gedefineerd in
`/etc/bind/named.conf.local`

*forward optie configuratie*
```
[...]
        forwarders {
             x.x.x.x;
             x.x.x.x;
        };

[...]
```
### Master DNS Zone Server
Om een DNS zone te defineren worden er 2 files gebruikt. 
1. Lookup File  (Naam --> IP)    
2. Reverse Lookup File (IP --> Naam)

De zone files staan ook in `/etc/bind`, deze files worden meestal vooraf gegaan
door `db.`, `db.local` is lookup file en `db.127` de reverse lookup file.

#### Lookup File

De lookup file moet minimaal 3 zone entries bevatten, deze 3 hebben allemaal
een verschillende record type. Een DNS zone entry heeft de volgende opbouw.

|name   |ttl    |record class   |record type    |record data    |
|--     |--     |--             |--             |--             |

De 3 nodige record types zijn:
1.  SOA  
    Start of Authority Record. Definitie van de Zone.
2.  NS  
    Nameserver gekoppeld aan de zone.
3.  A  
    Adres record voor de zone.

Voor meer info zie volgende lijst van mogelijke [DNS record
types](https://en.wikipedia.org/wiki/List_of_DNS_record_types).

```
;
; BIND data file for servermanagement
;
$TTL    3h
@       IN      SOA     ns1.servermanagement. admin.servermanagement. (
                          1        ; Serial
                          3h       ; Refresh after 3 hours
                          1h       ; Retry after 1 hour
                          1w       ; Expire after 1 week
                          1h )     ; Negative caching TTL of 1 day
;
@       IN      NS      ns1.servermanagement 

@                       IN      A       xxx.xxx.xxx.xxx
ns1                     IN      A       xxx.xxx.xxx.xxx 
www                     IN      CNAME   servermanagement.
``` 
### Reverse Lookup File

De reverse lookup file zorgt ervoor dat we een ip kunnen matchen naar een
domein naam. Dit is niet noodzakelijke file, het kan wel handig zijn voor 
systeeem administrators voor het troubleshooten.

```
;
; BIND data file for servermanagement
;
$TTL    3h
xxx.xxx.xxx.in-addr.arpa.     IN      SOA     ns1.servermanagement. admin.servermanagement. (
                          1        ; Serial
                          3h       ; Refresh after 3 hours
                          1h       ; Retry after 1 hour
                          1w       ; Expire after 1 week
                          1h )     ; Negative caching TTL of 1 day
;
       IN      NS      ns1.servermanagement 

xxx.xxx.xxx.in-addr.arpa.   IN    NS      ns1.servermanagement. 
```

###bind9 configuratie

Om de zone file in te laden in bind9, moet de file gesourced worden. Dit
gebeurd door volgende entry toe te voegen aan `named.conf.local`

```
[..]
zone "servermanagement" {
       type master;
       file "/etc/bind/db.servermanagement";
};

[..]
```

Als dit gebeurd, kan de DNS server opnieuw worden opgestart en is de DNS zone
geconfigureerd.


## DNS Server Distributie
Het IP van de DNS server kan op 2 verschillende manieren worden gedistrueerd.
1. Door een DHCP server
2. Door een handmatige instelling.

Voor een handmatige instelling op linux plaatsen we er volgende de interface
configuratie de volgende lijn er bij. 

`dns-nameserver xxx.xxx.xxx.xxx`
## Links 
* https://help.ubuntu.com/community/BIND9ServerHowto
* https://linuxconfig.org/linux-dns-server-bind-configuration
* https://en.wikipedia.org/wiki/Zone_file










