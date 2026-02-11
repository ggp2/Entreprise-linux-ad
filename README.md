## Architecture Linux d’entreprise avec services critiques centralisés et authentification Active Directory
- Mise en place des services d’infrastructure sous Linux (DNS, DHCP, NTP, Samba, mail, db)
- Authentification centralisée des systèmes Linux et Windows via Active Directory
- Intégration des machines Linux au domaine AD (SSSD, Kerberos)
- Supervision de l’infrastructure (monitoring Linux)
- Mise en œuvre des stratégies de sauvegarde et restauration
- Virtualisation de l’environnement avec KVM

## Objectif du projet



#  Infrastructure Linux / Windows – Providence.lan

##  Description

Ce projet présente la mise en place d’une infrastructure Linux avec authentification centralisée via Active Directory windows et services réseau intégrés.

Objectif : simuler une infrastructure d’entreprise complète (on-premise).
D'autre service seront a ajouté a l'instar les sql server, docker, kubernete...

---

## ⚙️ Architecture

Réseau : 192.168.10.0/24

| Serveur  | OS             | Rôle        | IP            |
|----------|----------------|-------------|---------------|
| server01 | RHEL 9         | DNS / DHCP  | 192.168.10.10 |
| dc1      | Windows Server | AD DS       | 192.168.10.15 |
| mail     | CentOS 7       | Mail Server | 192.168.10.30 |
| files    | Ubuntu 22.04   | Samba       | 192.168.10.50 |
| monitor  | Ubuntu 22.04   | Zabbix      | 192.168.10.20 |
|web       |Ubuntu 22.04    |             |
Accès Internet via hotspot mobile (NAT).

---

## 🧩 Services Déployés

### 🔹 Active Directory
- Domaine : providence.lan
- Gestion centralisée des utilisateurs
- Kerberos / LDAP

### 🔹 DNS (BIND9)
- Zone interne
- Enregistrements AD (SRV)
- Résolution interne/externe

### 🔹 DHCP
- Attribution dynamique
- Réservations serveurs
- Options DNS/Gateway

### 🔹 Intégration Linux / AD
- realmd / sssd / kerberos
- Authentification centralisée
- Home auto

### 🔹 Samba (Fichiers)
- Partages sécurisés
- ACL AD
- Authentification domaine

### 🔹 Messagerie
- Postfix (SMTP)
- Dovecot (IMAP/LMTP)
- Authentification AD
- Maildir

### 🔹 Supervision
- Zabbix Server
- Agents Linux/Windows
- Monitoring services

---

## 🔐 Sécurité

- FirewallD
- SELinux
- PAM + SSSD
- Permissions Unix

---

##  Technologies

- Linux : RHEL 9 / CentOS 7 /Ubuntu 22.04
- Windows Server 2016
- Active Directory
- BIND9 / DHCP
- Postfix / Dovecot
- Samba
- Zabbix
- Git

---

##  Compétences Développées

✔️ Administration Linux  
✔️ Intégration AD  
✔️ DNS/DHCP  
✔️ Messagerie  
✔️ Supervision  
✔️ Troubleshooting  
✔️ Sécurité système  

---

## 📂 Structure du dépôt

```bash
