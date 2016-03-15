# Les 5: File Server

Op linux zijn er 2 populaire file servers, Samba en NFS. Samba is de gereversd
geengineerde versie van SMB een propetair file sharing protocol van windows. 
NFS is een file sharing protocol ontwikkeld door Sun Microsoft, dit is vooral
ondersteund op Linux. Het is mogelijk NFS in te stellen op Windows. Dit is
echter lastig.

Samba / SMB is makkelijk te in te stellen op Windows als op Linux. Het doel van
dit labo is om een Samba server in te stellen op een Linux machine. De geshared
folders kunnen dan als netwerk drive gemount worden op het host. 

De file server zal ook voorzien worden van een back up systeem gebaseerd op cronjobs. 

**Zie dat er verbinding is tussen de host en de guest**

## File Server

Samba heeft de volgende pakketen nodig:
* samba 
* samba-common 

Installeer eerst deze.

De samba configuratie file bevindt zich op volgende locatie:  
**/etc/samba/smb.conf**

Deze configuratie file bestaat uit verschillende sectie die worden aangeven door
square brackets. Er zijn enkele vooraf gedefinieerde secties als ook custom secties voor shares gedefinieerd door de user. De standaard secties zijn:

*   **[global]**  
    Hier worden de algemene  settings van de samba server bewaard.
*   **[homes]**
    Er wordt ook een standaard sectie voorzien voor het delen van de home directories van de user.
*   **[printers]**  
    Samba kan ook gebruikt worden voor het delen van printers. Deze sectie is
    voor dit labo niet van toepassing.


Het is dus ook mogelijk om een sectie te voor zien die eender welke map kan delen. Deze wordt gedefinieerd in een aparte sectie.

voorbeeld van een custom samba sectie:
```
[secured]
 path = /samba/secured
 valid users = @smbgrp
 guest ok = no
 writable = yes
 browsable = yes
```
*   **path**  
    De locatie die gedeeld word door de share 
*   **valid users**
    De toegang wordt gedefineerd door het toewijzen van een groep aan de share.
*   **guest ok**  
    Het is niet toegelaten om anomyous te verbinden
*   **writable**
    Toekennen van remote schrijfrechten

Eens je webserver is herstart kan je de secured share accessen met windows
explorer door te navigeren naar ``\\xxx.xxx.xxx.xxx\secured``.

## Cron

Cron is een task scheduler op linux. cron stels ons instaat om op een
specifiek moment een bepaald commando / script uit te voeren. Cron wordt
uitgevoerd door de entries in de crontab, m.a.w. crontab is de configuratie 
utility van cron.

Crontab heeft 3 mogelijke optie switches:
*   **crontab -l**  
    Met dit commando kan je oplijsten welke cronjobs er momenteel in de crontab
    zitten.
*   **crontab -e**  
    Met dit commando kan je de crontab editen.
*   **crontab -r**  
    Met dit commando kan je de huide crontab verwijderen. 

cronjob heeft de volgende syntax 
```
┌───────────── min (0 - 59) 
│ ┌────────────── hour (0 - 23)
│ │ ┌─────────────── day of month (1 - 31)
│ │ │ ┌──────────────── month (1 - 12)
│ │ │ │ ┌───────────────── day of week (0 - 6)
│ │ │ │ │
│ │ │ │ │
* * * * * * command to execute 

ex:

15 3 * * 1-5 find "$HOME" −name core −exec rm −f {} + 2>/dev/null
0 12 14 2 * mailx john%Happy Birthday!%Time for lunch.

```

**crontab is user specifiek**
