# Remote Management

## SSH

Je kan een machine op afstand configuren over Secure Shell protocol. Secure
Shell opent een beveiligde tunnel naar de target computer zodat je een remote
terminal kan draaien, nu is het mogelijk om alle commando's die je op het
machine kan uitvoeren rechtstreeks van op het target machine draaien.

*Uit de manpage van SSH:*
> ssh  (SSH client) is a program for logging into a remote machine and for 
> executing commands on a remote machine.  It is intended to replace rlogin and
> rsh, and provide secure encrypted communications  between  two  untrusted 
> hosts over an insecure network.  X11 connections, arbitrary TCP ports and 
> UNIX-domain sockets can also be forwarded over the secure channel. ssh 
> connects and logs into the specified hostname (with optional  user  name).
> The  user  must prove his/her identity to the remote machine using one of 
> several methods depending on the protocol version used (see below). If 
> command is specified, it is executed on the remote host instead of a login
> shell.

*Voor meer info zie: man ssh*

## SSH Tools

Als je van op een Windows machine werkt kan je een SSH verbinding aangaan met
volgende programma:

* **PuTTY + PuTTYgen:** 2 Windows tools waarmee je SSH verbindingen kunt maken en
  keys kunt genereren, het bevat wel niet het ssh-copy-id programma.
* **Cygwin:** Een verzameling van open source en linux tools waardoor je een linux
  terminal kan emuleren in je Windows omgeving
* **MobaXterm:** Een all in one suite voor het opzetten van ssh verbinding, het
  maakt ook gebruik van een terminal emulator, als je de installer versie
  gebruikt.

*MobaXterm is de meest complete oplossing, cygwin geeft je een linux feeling en
PuTTy is eenvouding*

Een SSH server oplossing voor is niet echt aangeraden, remote monitoring van
een windows systeem word gedaan met een GUI oplossing.

Op linux zijn de SSH tools beschikbaar in een terminal. De server applicatie ontbreek meestal op desktop distributies. Deze kan geïnstalleerd worden met de **openssh-server** package.

## Opzetten van SSH connectie

Voor dat we een SSH verbinding met het target kunnen opzetten moeten we eerst
volgende voorwaarden voldoen zijn:
* Er is een netwerk verbinding tussen onze remote client (client) en het target
  machine (server). (Er kan gepinged worden tussen beide machines.)
* openssh-server is geïnstalleerd op het target machine

Als alle voorwaarden zijn voldaan, dan kan er met een user account van het
target machine vanaf een remote client worden ingelogd. 

Hiervoor gebruiken we  een van de volgende commando's:

* `ssh username@hostname`
* `ssh username@x.x.x.x`

Waarbij hostname een een URL is van een specifieke server en x.x.x.x een ip
adres naar een specifieke server. 

## Gebruiken van SSH Keys

Het is mogelijk om aan te melden op de SSH server door middel van public-key
cryptografie en challenge respons authenticatie. Het grootste voordeel van dit
systeem is dat je nooit je paswoord over het netwerk moet sturen. Hierdoor kan
het paswoord niet worden onderschept en gekraakt worden. Het paswoord wordt
dus niet in plain text door gestuurd maar kan nog steeds gekraakt worden. Het
stopt ook de mogelijkheid op brute force aanvallen op de SSH server als de
paswoord login gedisabled zijn.

### ssh-keygen

Eerst moet er een keypair worden aangemaakt. Dit kan met het programma SSH keygen, deze maakt standaard een paar RSA sleutels aan. 

*NOOT: Voor dat je een key installeerd, moet je acces hebben aan je target
machine, dit door een passwoord login of fysieke acces*

Op je remote machine, het machine waarmee je passwordless acces wilt tot aan je
machine, roep je het commando `ssh-keygen` aan. Dit zal nog 2 vragen stellen:

* **locatie van de keys:** De keys worden als text bestand bewaard. Hier kan
  een folder meegeven waar je d keys wil bewaren. De default locatie is
  `~/.ssh/`. Hier worden de beide keys bewaard. Je kan deze default laten.
* **passphrase:** De keys worden in plain text bewaard, je kan deze encrypteren
  indien gewenst. Als je dit veld leegt laat dan blijven de keys in plain text.

### ssh-copy-id

De laatste stap voor acces met een public-key is het kopiëren van deze key. Dit
kan met ssh-copy-id of een manueel kopiëren van de key. Er is dus toegang nodig
tot het target machine. Om de key te pokeren gebruik je volgende commando,
`ssh-copy-id user@targetmachine`  

### openssh-server configuratie

* **/etc/ssh/ssh_config:** globale user configuratie, deze configuratie word
  gebruik als `~/.ssh/config` ontbreekt.
* **/etc/ssh/sshd_config:** De configuratie voor de SSH server daemon
* **~/.ssh/config:** Een specifieke ssh user config 
 
### manpages

Zie de volgende man pages voor meer informatie over SSH

* man ssh
* man ssh_config
* man sshd
* man sshd_config













