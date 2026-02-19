
# Server01 – DNS \& DHCP Infrastructure

## Presentation 
Le serveur \*\*server01.providence.lan\*\* assure les services fondamentaux de résolution de noms et d’attribution d’adresses IP de facon dynamique pour l’infrastructure interne.
Il joue un rôle central dans l’intégration entre les serveurs Linux et le contrôleur de domaine Windows Active Directory


---

## Information Generale

| Élément    | Valeur                   |
|------------|--------------------------|
| Hostname   | server01.providence.lan  |
| Adresse IP | 192.168.10.10            |
| OS         |  RHEL 9                  |
| Rôles      | DNS Master, DHCP Server  |
| Domaine    | providence.lan           |

---

## Services déployés

### DNS – BIND9

- Serveur DNS autoritatif pour le domaine `providence.lan`
- Gestion des zones directe et inverse
- Support des enregistrements SRV pour Active Directory
- Résolution récursive pour le réseau interne

###  DHCP – ISC DHCP Server

- Attribution dynamique des adresses IP
- Distribution automatique du DNS et du domaine
- Configuration adaptée à l’environnement Active Directory  

---
## Fichiers Principaux 
Ces fichiers assurent la gestion centralisée de l’attribution des adresses IP
et de la résolution des noms au sein du réseau interne.

- `/etc/dhcpd/dhcpd.conf`  
  Configuration du serveur DHCP pour l’attribution dynamique des adresses IP.

- `/etc/named.conf`  
  Fichier principal de configuration du service DNS (BIND9).

- `/var/named/providence.lan.zone`  
  Zone directe pour la résolution des noms vers les adresses IP.

- `/var/named/10.168.192.rev`  
  Zone inverse pour la résolution des adresses IP vers les noms de domaine.

- `/etc/resolv.conf`  
  Configuration du résolveur DNS utilisée par le système.

Ces fichiers permettent d’assurer une communication fiable entre les serveurs,
le contrôleur de domaine et les postes clients.

## Synchronisation Horaire (NTP)

Le serveur utilise Chrony synchronisé sur le contrôleur de domaine.

Source principale :
- 192.168.10.15 (DC1)

Objectif :
- Stabilité Kerberos
- Authentification AD fiable
- Pas de dérive temporelle

Validation :
chronyc sources -v
chronyc tracking












