\# Server01 – DNS \& DHCP Infrastructure



\##  Présentation

Le serveur \*\*server01.providence.lan\*\* assure les services fondamentaux de

résolution de noms et d’attribution d’adresses IP pour l’infrastructure interne.



Il joue un rôle central dans l’intégration entre les serveurs Linux et

le contrôleur de domaine Windows Active Directory.



---



\## 🖥️ Informations générales



| Élément | Valeur |

|---------|---------|

| Hostname | server01.providence.lan |

| Adresse IP | 192.168.10.10 |

| OS | Rocky Linux / RHEL 9 |

| Rôles | DNS Master, DHCP Server |

| Domaine | providence.lan |



---



\##  Services déployés



\### DNS – BIND9

\- Serveur DNS autoritatif pour le domaine `providence.lan`

\- Gestion des zones directe et inverse

\- Support des enregistrements SRV pour Active Directory

\- Résolution récursive pour le réseau interne



Fichiers principaux :



---



\###  DHCP – ISC DHCP Server

\- Attribution dynamique des adresses IP

\- Distribution automatique du DNS et du domaine

\- Configuration adaptée à l’environnement Active Directory









