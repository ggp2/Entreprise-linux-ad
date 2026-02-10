# Server06 – Monitoring (Zabbix)

##  Rôle
Serveur de supervision centralisée de l’infrastructure \*\*providence.lan\*\*(Zabbix Server + Frontend + DB MariaDB).

##  Informations système

| Élément         | Valeur                    |
|-----------------|---------------------------|
| Hostname        | server06                  |   
| OS              | Ubuntu 24.04.3 LTS        |
| Hyperviseur     | VirtualBox                |
| Zabbix          | 7.0.22                    |
| Base de données | MariaDB                   |
| Réseau LAN      | 192.168.10.20/24 (enp0s8) |
| Réseau NAT      | 10.0.2.15/24 (enp0s3)     |

##  Architecture réseau
- \*\*Interface LAN (192.168.10.0/24)\*\* : collecte des métriques depuis les serveurs internes (AD, DNS/DHCP, Samba…)
- \*\*Interface NAT (10.0.2.0/24)\*\* : accès Internet pour mises à jour OS et paquets Zabbix

##  Preuves de fonctionnement


### Zabbix Server

```bash
systemctl status zabbix-server --no-pager
zabbix\_server --version
```
##Périmètre de supervision (exemples) 
DC1 : disponibilité, ports AD (88/389/445), charge système, événements critiques
server01 : DNS (53 TCP/UDP), DHCP (67 UDP), disponibilité du service named
server07 : Samba/Winbind, port 445, espace disque /srv/samba

##Dossiers

zabbix-server/ : installation \& configuration Zabbix Server
agents/ : déploiement agents Linux/Windows + checklist
templates/ : items et dashboards orientés services (AD/DNS/Samba)
troubleshooting/ : incidents et correctif



