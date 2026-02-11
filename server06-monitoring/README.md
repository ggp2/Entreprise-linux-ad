# Zabbix Monitoring Lab (Enterprise-style)

Lab de supervision type entreprise basé sur **Zabbix 7.0.22**, intégrant :
- Zabbix Server + Frontend Web (Apache2)
- Base de données **MariaDB locale** (bind localhost)
- Agents Zabbix sur hôtes Linux et Windows
- Documentation d’installation, configuration, validation, troubleshooting
- Captures de dashboards et templates

## Objectifs
- Mettre en place une supervision complète (disponibilité, performance, services)
- Appliquer des pratiques “production-like” : séparation des rôles, durcissement, tests, dépannage documenté

---

## Architecture

### Plan IP & rôles
| Machine    | Rôle                 | OS                 | IP            |
|------------|----------------------|--------------------|---------------|
| server01   | DNS / DHCP           | RHEL 9             | 192.168.10.10 |
| dc1        | Contrôleur AD        | Windows Server 16  | 192.168.10.15 |
| mail       | Serveur Mail         | CentOS 7           | 192.168.10.30 |
| files      | Serveur Fichiers     | Ubuntu 24.04.3 LTS | 192.168.10.30 |
| monitor    | Supervision (Zabbix) | Ubuntu 24.04.3 LTS | 192.168.10.20 |
| passerelle | NAT / Internet       | Hotspot Tel        | 192.168.10.1  |

> Le serveur **monitor** utilise un second réseau NAT pour les mises à jour (ex: 10.0.2.15/24).

### Schéma
Voir: 

---
## Stack technique
- **Zabbix**: 7.0.22
- **OS Monitor**: Ubuntu 24.04.3 LTS
- **Frontend**: Apache2
- **DB**: MariaDB (local)  
  - bind-address: `127.0.0.1`
  - charset: `utf8mb4`

---

## Installation (Quickstart)
1. Prérequis: `installation/prerequisites.md`
2. MariaDB: `installation/install-mariadb-local.md`
3. Zabbix Server: `installation/install-zabbix-server-ubuntu24.md`
4. Apache/Frontend: `installation/install-apache-frontend.md`
5. Agents:
   - Linux Agent2: `agents/install-linux-agent2.md`
   - Windows Agent2: `agents/install-windows-agent2.md`

---

## Validation
Checklist de vérification: `validation/checks.md`

---

## Troubleshooting (incidents documentés)
- Port 10050 déjà utilisé: `troubleshooting/port-10050-in-use.md`
- Agent down / unreachable: `troubleshooting/agent-down.md`
- Erreurs DB/permissions: `troubleshooting/db-errors.md`

---

## Captures / preuves
Dashboards: `dashboards/screenshots/`

---

## Sécurité (résumé)
- DB locale uniquement (pas exposée au LAN)
- Ports Zabbix contrôlés (10051 server, 10050 agents)
- Approche “least exposure” (pare-feu + segmentation)

Voir: `docs/security.md`

---

## Licence
MIT (optionnel)
