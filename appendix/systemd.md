# systemd 
systemd is een system en service manager voor Linux, compatibel met SysV en LSB
init scripts, systemd voorziet geavanceerde parallellisatie capaciteiten om
services te starten, voorziet het on-demand controle over het starten, stoppen
en het weergeven van data over processen.

## Vaak gebruikte systemd commands:**

* systemctl disable sshd
* systemctl enable sshd
* systemctl start sshd
* systemctl stop sshd
* systemctl restart sshd
* systemctl reload sshd
* systemctl status sshd

start/stop: starten en stoppen van de service. enable/disable: automatisch
starten van een service bij het booten van het systeem. reload voor herstarten
van een service. Status geeft de huidige staat weer van de service.

## journalctl

journalctl is het logging systeem van systemd en vervangt de syslog daemon. Enkele nuttige commando's voor journalctl zijn.

* journalctl -e      # end
* journalctl -f      # follow
* journalctl -b      # this boot
* journalctl -u sshd # unit
