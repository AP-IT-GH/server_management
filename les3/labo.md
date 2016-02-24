# Labo: FTP

## Opdracht

* Installeer vsftp  op je server
* Installeer FileZilla in je Windows Omgeving
* Snif met Wireshark naar een paswoord van ftp user
* Maak de directory `/var/www` aan, geef lees en schrijfrechten aan de www
  groep.
* Voeg de helft van de developers toe aan de www groep (Eerste twee.)
* Voer elke `www` user volgende commando uit:  
  `sudo mount --bind /var/www /home/www_user/www`
* Configureer FTP volgens volgende requirements:
    * De sysadmin groep wordt niet in een chroot omgeving ingelogd.
    * De developer groep logt in een chroot omgeving

## Verslag

* Toon het tcp/ip packet met paswoord (screenshot).
* Wat is de output van `pwd` tidens een ftp sessie met een www user.
* Wat is de output van `ls /` tijdens een ftp sessie van een sysadmin user.
* Wat is FTPS en wat is het verschil met SFTP

## BONUS

* Hoe configureer je FTPS.
