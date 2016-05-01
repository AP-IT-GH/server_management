# Les 8: Integratie
## Opdracht
Voor dit labo worden de voorgaande server technologieën met elkaar
geïntegreerd. Hiervoor zijn er meerdere virtuele machines nodig. 

Om deze virtuele machine te faciliteren, zal er in groepen van 3 personen
gewerkt worden.

Elke persoon zal minstens een specifieke machine hosten, deze zullen met een
fysieke switch verbonden zijn. De machines zijn als volgt:

* Server #1:
    * FTP
    * Webserver
    * SSH

* Server #2:
    * DNS
    * SSH

* Server #3:
    * DHCP
    * SSH 

* Cliënt #1:  
Deze zal de verbinding maken met alle server. Op dit machine moet alleen de
cliënt voor de geïnstalleerd servers installeren. De cliënt zal een Ubuntu
desktop versie zijn.


Op de cliënt zullen volgende commando's worden uitgevoerd:
* SSH:
    * `ssh user@dhcp.groepnaam.be`
    * `ssh user@dns.groepnaam.be` 
    * `ssh user@groepnaam.be`
    * `scp -r /var/www user@groepnaam.be:/var/www`

> De `user` is een non root user naar eigen keuze op het systeem.

* DHCP:
    * `sudo dhclient -r`
> Het is de de bedoeling dat de cliënt een IP krijgt van de DHCP server.

* DNS:  
    * `dig groepnaam.be`

* FTP:
    * `ftp ftp.groepnaam.be`

* Web:  
De website die wordt weergegeven is degene die gekopieerd werd met het commando
`scp -r /var/www user@groepnaam.be:/var/www`

Heel dit geeft volgend netwerk diagram:

                                 +-------Fysieke PC #1------+
                                 | +----------------------+ |
                                 | |                      | |
                                 | |    FTP / Webserver   | |
                                 | |                      | |
                                 | +----------------------+ |
                                 +--------------------------+
                                              |
    +-------Fysieke PC #2------+              |
    | +----------------------+ |   +----------+-----------+
    | |                      | |   |                      |
    | |    DNS Server        +-----+    Switch            +------------------+
    | |                      | |   |                      |                  |
    | +----------------------+ |   +----------+-----------+                  |
    +--------------------------+              |                              |
                                              |                              |
                                 +------Fysieke PC #3------------------------------------+
                                 | +----------------------+     +----------------------+ |
                                 | |                      |     |                      | |
                                 | |    DHCP Server       |     |   Client             | |
                                 | |                      |     |                      | |
                                 | +----------------------+     +----------------------+ |
                                 +-------------------------------------------------------+



## Verslag

Voor een cijfer te krijgen voor dit labo moeten de bovenstaande commando's
worden uitgevoerd in het bijzijn van de lector.

Er moet maar 1 verslag worden geupload worden per groep. Naam en leden duidelijk vermelden.


* Aangepast netwerk diagram met IP en netwerk kaart configuratie van de
  virtuele machine.
* De volgende map met specifiek inhoud.
```
src/
├── client1
│   ├── interfaces
│   └── resolv.conf
├── server1
│   ├── interfaces
│   ├── sshd_config
│   ├── vsftpd.conf
│   └── website_config_file
├── server2
│   ├── db.groepnaam
│   ├── interfaces
│   ├── named.conf.local
│   └── sshd_config
└── server3
    ├── dhcpd.conf
    ├── interfaces
    └── sshd_config

```


 



