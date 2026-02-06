\# Zabbix Monitoring



Supervision d’une infrastructure locale (Linux/Windows services) avec \*\*Zabbix\*\* : disponibilité, ressources système, services critiques, alerting et dashboards.



\## Objectif

Mettre en place une supervision centralisée sur un serveur dédié (`monitor`) pour surveiller l’état des hôtes et services d’un domaine interne `providence.lan`.



\## Architecture

| Host                    | Rôle              | IP            |

|-------------------------|-------------------|---------------|

| server01.providence.lan | DNS / Infra       | 192.168.10.10 |

| dc1.providence.lan      | Active Directory  | 192.168.10.15 |

| monitor.providence.lan  | ZabbixS +Frontend | 192.168.10.20 |

| files.providence.lan    | File Server       | 192.168.10.30 |

| mail.providence.lan     | Mail Server       | 192.168.10.40 |

| www.providence.lan      | Web Server        | 192.168.10.50 |

| vpn.providence.lan      | VPN Server        | 192.168.10.60 |



\## Stack

\- Zabbix Server + Frontend Web

\- MariaDB

\- Zabbix Agent (Linux)

\- (Option) Zabbix Agent2 / Windows Agent pour `dc1`



\## Installation (résumé)

\- Installer Zabbix Server sur `monitor`

\- Installer Zabbix Agent sur chaque hôte

\- Ajouter les hôtes dans Zabbix + appliquer les templates

\- Configurer alertes (CPU/RAM/DISK/Host down/Service down)



\## Supervision

\- Disponibilité des hôtes (ICMP)

\- Ressources : CPU, RAM, Disque, Load, Réseau

\- Services : SSH (22), DNS (53), HTTP/HTTPS (80/443), SMTP (25), LDAP (389), Kerberos (88), VPN (port selon service)



\## Alerting (exemples)

\- Host down : immédiat

\- Disque > 80%

\- CPU > 90%

\- Service down : immédiat



\## Démo / preuves

Captures d’écran : `docs/screenshots/`

Tests : `tests.md`



\## Compétences mises en œuvre

Linux, réseau TCP/IP, supervision Zabbix, agents, templates, triggers, alerting, documentation.



