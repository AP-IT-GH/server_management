# FTP Server
File Transfer Protocol is een applicatie laag netwerk protocol om data te
versturen tussen computers op een netwerk. FTP maakt gebruikt van een client
server model. 

FTP kan gebruikt worden in anonymous mode. In deze mode is het niet nodig om
ogin credentials te gebruiken.

FTP is geen veilig protocol. Het is mogelijk om de login gegevens plain text te sniffen door gebruik te maken van Wireshark.


## FTP Software
### FTP Server

* bftpd — Small, easy-to-configure FTP server
* proFTPd — A secure and configurable FTP server
* Pure-FTPd — Free (BSD-licensed), secure, production-quality and
  standard-compliant FTP server.
* **vsftpd — Lightweight, stable and secure FTP server for UNIX-like systems.**

vsftpd is de default ftp server applicatie voor verscheidende linux
distributies. Daarom zullen voor dit labo gebruik maken van **vsftpd**. 

Installeer vsftp op je ubuntu server.

De configuratie file voor vsftpd is te vinden in de /etc/ folder.


### FTP Client

* CurlFtpFS — Filesystem for accessing FTP hosts; based on FUSE and libcurl.
* FatRat — Download manager with support for HTTP, FTP, SFTP, BitTorrent,
  RapidShare and more.
* **FileZilla — Fast and reliable FTP, FTPS and SFTP client.**
* fuseftp — FTP filesystem written in Perl, using FUSE.
* gFTP — Multithreaded FTP client for Linux.
* LFTP — Sophisticated command-line FTP client.
* LftpFS — Read-only filesystem based on lftp (also supports HTTP, FISH, SFTP,
  HTTPS, FTPS and proxies).
* ncftp — A set of free application programs implementing FTP.
* tnftp — FTP client with several advanced features for NetBSD.

De meeste opties zijn beschikbaar voor Linux distributies, **FileZilla** is een
cross platform oplossing. Ik raad aan dit te gebruiken als client. Andere
client applicaties zijn toegelaten. Een cli ftp client applicatie is ook
default beschikbaar op linux en Windows.

De meeste webbrowser ondersteunen filebrowsing op een ftp server.


## chroot
chroot is een linux operatie dat de de root directory voor het process van een
applicatie veranderd. Als ook de de subprocessen die worden gelanceerd van uit
process in een nieuwe chroot omgeving. Zo een nieuwe chroot omgeving word een
chroot jail genoemd.

Een praktisch voorbeeld:
Bij ftp kan er ook gebruik gemaakt worden van een chroot jail. Dit wordt meestal gedaan op de home folder van een user.

Normaal gezien als we het commando `cd /` uitvoeren gaan we naar de root
directory van het systeem. Maar als we inloggen op een *chroot jail* ftp sessie
op basis van de home directory van de user, komen we ineens op de root
directory van het chroot jail. We kunnen dan niet naar een hogere directory
navigeren. Dus als we het commando `cd /` uitvoeren, navigeren we naar de root
directory maar voor het bovenliggende systeem van het huidige process heeft
deze root directory het volgende path `/home/currentuser`

Dit is heeft als voordeel dat we een soort sandbox creëren. Hierdoor is het
eenvoudiger om een applicatie te testen zonder dat het onderliggende systeem
wordt blootgesteld. 








