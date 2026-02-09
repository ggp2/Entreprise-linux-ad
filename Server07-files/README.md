# Server07 – Serveur de Fichiers Samba Intégré à Active Directory

##  Présentation

Ce serveur assure le rôle de serveur de fichiers centralisé au sein du domaine
Active Directory **providence.lan**, avec authentification centralisée
via Samba et Winbind.

Il permet aux utilisateurs du domaine d’accéder aux ressources partagées
en utilisant leurs identifiants Active Directory.

---

##  Objectifs

- Intégrer un serveur Linux dans un domaine Active Directory
- Centraliser les partages réseau
- Gérer les accès via les groupes AD
- Assurer une authentification sécurisée
- Mettre en place une infrastructure proche d’un environnement réel

---

##  Informations Système

| Élément    | Valeur                  |
|------------|-------------------------|
| Hostname   | server07.providence.lan |
| Adresse IP | 192.168.10.50           |
| OS         | Ubuntu 24.06            |
| Domaine    | providence.lan          |
| Rôle       | Serveur de fichiers     |

---

##  Technologies Utilisées

- Samba
- Winbind
- Kerberos
- DNS ( server01)
- Active Directory ( server02)
- NTP / Chrony / Timesyncd

---

##  Structure du Dossier


| Fichier           | Description                    |
|-------------------|--------------------------------|
| smb.conf          | Configuration Samba principale |
| shares.md         | Documentation des partages     |
| integration-ad.md | Procédure d’intégration AD     |

---

##  Configuration Principale

Le serveur utilise une configuration Samba en mode ADS :

- Authentification Kerberos
- Intégration Winbind
- Mapping UID/GID automatique
- Gestion ACL Windows

Extrait :

```ini
security = ADS
realm = PROVIDENCE.LAN
workgroup = PROVIDENCE
```
##  integration au Domaine
la jointure est realisé  via  : net ads join -U Administrateur

## Tests de Validation
- Authentification Kerberos
- wbinfo -t
- wbinfo -u
- wbinfo -g
- getent passwd Administrateur

## Dépannage et Résolution
les Principaux probleme rencontrés

| Problème        | Cause                     | Solution             |
| --------------- | ------------------------- | -------------------- |
| Erreur Kerberos | Désynchronisation horaire | Configuration NTP    |
| Winbind KO      | smb.conf invalide         | Correction syntaxe   |
| Join échoué     | DNS incorrect             | Correction DNS       |
| ACL inactives   | VFS absent                | Activation acl_xattr |








