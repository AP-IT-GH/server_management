# Les 4: Webserver
Als we van webservers spreken, dan hebben spreekt men over een solution stack.
Met alleen maar een webserver kunnen alleen maar een statische website
voorzien. Om een iets dynamische website te voorzien hebben we ook nog een 
server side scripting oplossing nodig. Als we nog data willen verwerken, is er
ook een database nodig.

Deze 3 voorzien samen met het operating systeem een solution stack.        
Enkele bekende solution stacks zijn:
* WIMP
    * Windows
    * Internet Information Services
    * MSSQL Server
    * PHP
* WAMP
    * Windows
    * Apache 
    * MySQL
    * PHP
* LAMP
    * Linux
    * Apache 
    * MySQL
    * PHP
* LEMP
    * Linux 
    * nginx (Engine X)
    * MySQL
    * PHP
* MEAN
    * Mongo
    * Express
    * Angular (frontend javascript framework)
    * Node.js

Dit zijn populaire stacks maar modules kunnen verwisselen. Voor het labo gaan
we **alleen maar een webserver installeren.** We gaan gebruik maken van
**nginx**.

## nginx

> nginx [engine x] is an HTTP and reverse proxy server, a mail proxy server,
> and a generic TCP proxy server, originally written by Igor Sysoev. For a long
> time, it has been running on many heavily loaded Russian sites including
> Yandex, Mail.Ru, VK, and Rambler. According to Netcraft, nginx served or
> proxied 24.86% busiest sites in February 2016. Here are some of the success
> stories: Netflix, Wordpress.com, FastMail.FM.
>
> -nginx website

### nginx configuratie

nginx configuratie bevind zich in de folder */etc/nginx/*

Daarin bevinden zich 3 belangrijke items.

1. nginx.conf (file):  
    Deze file bevat de algemene configuratie voor de nginx applicaties.
2. sites-available (folder):  
    Deze folder bevat de configuraties van de beschikbare website. Hierin 
    worden de configuratie bestanden in bewaard. De website is geconfigureerd
    maar is nog bereikbaar.
3. sites-enabled (folder):  
    De website config files die hier staan zijn beschikbaar voor de
    buitenwereld. Een softlink naar het bestand in de sites-available folder
    volstaat.  

Het is dus mogelijk om een meerdere website te serven met nginx. Zo een website
noemt een *nginx server block*

**voorbeeld site configuratie file**

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;
    server_name _;
    location / {
        try_files $uri $uri/ =404;
    }
}
```

uitleg keywords:

* listen:  
    listen bind een een socket (ip + poort number) aan de webserver. Als er 
    alleen een poort nummer saat dan luistert de server naar elk beschikbaar ip op 
    het machien. Het kan ook worden ingesteld om te luisteren naar ipv6 adres. 
* root:  
    root wijst naar de rootfolder van de website.
* index:  
    deze bevat de filename voor de default landing page voor de website.  
* server_name:  
    dit is de url voor de website (bv. example.com).
* location:  
    geavanceerde configuratie voor root/index, default configuratie is voor 404
    error.
   
## Statisch IP adres

Interfaces op een Ubuntu / Debian systeem worden gemanaged met de commando.
`ifup` en `ifdown`. Met `ifup` starten we een interface en met `ifdown` stoppen
we een interface. Mogelijke voorbeelden hiervan zijn:

* `sudo ifup eth0`
* `sudo ifdown eth3`

Het is ook mogelijk om een de status van de interfaces te controleren met
*systemd* Hiervoor gebruiken we volgende commando's:

* `sudo systemdctl start networking`
* `sudo systemdctl stop networking`
* `sudo systemdctl restart networking`

Net zoals alle andere configuraties op linux zijn de interfaces configuraties
text based. De configuraties files zijn te vinden in de folder */etc/network/*

Daarin hebben we 2 belangrijke items.

1. interfaces (file)
2. interfaces.d (folder)

De interfaces file is de file die default word ingeladen bij het starten van
het netwerk. Deze file bevat de configuratie voor loopback interface en sourced
de files van uit de interfaces.d folder. De interfaces.d folder bevat in
individuele bestanden, de configuratie voor elke interface. 

Als we een statisch ip adres willen instellen dan moeten er een config file
zijn voor de specifieke interface met volgende template:

```
auto iface_name 
iface iface_name inet static
    address xxx.xxx.xxx.xxx
    netmask xxx.xxx.xxx.xxx
```

## Bronnen
* [Tutorial nginx server block](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-14-04-lts)
* [nginx configuratie](https://www.linode.com/docs/websites/nginx/how-to-configure-nginx)
* [Static IP tutorial](http://www.tecmint.com/set-static-ip-address-in-ubuntu-15-10-server/)
* [man interfaces](http://manpages.ubuntu.com/manpages/wily/man5/interfaces.5.html)












