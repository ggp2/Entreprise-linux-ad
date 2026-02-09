## Server02 – Active Directory Domain Services (AD DS)

#  Infrastructure Active Directory Linux & Windows

##  Présentation

Ce projet présente la conception et la mise en œuvre d’une infrastructure
informatique d’entreprise basée sur Linux et Windows Server, intégrant
un domaine Active Directory avec services réseau centralisés.

L’objectif est de simuler un environnement professionnel réel
pour le développement de compétences en administration systèmes et réseaux.

---

##  Objectifs

- Mettre en place un domaine Active Directory fonctionnel
- Centraliser l’authentification Linux / Windows
- Déployer des services réseau sécurisés
- Assurer la disponibilité et la maintenabilité
- Documenter l’infrastructure

---

##  Architecture Générale

| Serveur  | Rôle                  | IP            |
|----------|-----------------------|---------------|
| server01 | DNS / DHCP (Linux)    | 192.168.10.10 |
| dc1 	   | Contrôleur AD (Windows)| 192.168.10.15|
| server03 | Web / App             | 192.168.10.20 |
| server04 |                       | 192.168.10.30 |
| server05 | Messagerie            | 192.168.10.2 0|
| server06 | Monitoring / Backup   | 192.168.10.154|
| server07 | Fichiers (Samba)      | 192.168.10.50 |

---

##  Technologies Utilisées

### Systèmes
-  RHEL 9
- Ubuntu Server 22.04
- Windows Server 2016

### Services
- Active Directory (AD DS)
- DNS (BIND9)
- DHCP
- Samba / Winbind
- Kerberos / SSSD
- Apache / PHP
- Postfix / Dovecot
- OpenVPN / WireGuard
- Zabbix

### Virtualisation
- VirtualBox (environnement on-premise)

---

##  Structure du Projet

```bash
.
├─- architecture/
├── server01-dns-dhcp/
├── server02-ad-ds/
├── server03-/
├── server04-/
├── server05-mail/
├── server06-monitoring/
├── server07-samba/
└── docs/

## Sécurité

-Authentification centralisée AD 

-Kerberos pour Linux

-Groupes AD pour contrôle d’accès

-Pare-feu et VPN

-Séparation des rôles serveurs

## Fonctionnalités Principales

-Domaine Active Directory opérationnel
-DNS Linux externe à AD
-Jointure Linux via SSSD/Winbind
-Partages réseau sécurisés
-Messagerie interne
-Supervision réseau
-Accès distant VPN

##Documentation

###Chaque serveur dispose d’une documentation dédiée :
-Installation

-Configuration

-Dépannage

-Bonnes pratiques

Voir le dossier /docs.

### Validation & Tests

dcdiag

nslookup / dig

kinit / klist

wbinfo

realm list

Tests Samba

Tests VPN

### Perspectives d’Amélioration

-Haute disponibilité (HA)

-PKI interne

-MFA

-Sauvegarde centralisée

-Monitoring avancé

-Cloud hybride
