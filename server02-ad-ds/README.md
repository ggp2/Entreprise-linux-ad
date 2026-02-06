\# Server02 – Active Directory Domain Services (AD DS)



\## 📌 Présentation

Ce serveur héberge le contrôleur de domaine principal (DC1) de

l’infrastructure `providence.lan`. il y a qu 'un seul controleur de domain ( en entreprise il est necessaire d'avoir un second controleur de domaine) 



Il assure l’authentification centralisée, la gestion des utilisateurs, des groupes et l’intégration des serveurs Linux.



Il sied de noté que que le ce serveur n'auras pas de configuration DNS car déjà configurer sur le server01



---



\##  Informations générales



| Élément    | Valeur  |

|---------   |---------|

| Hostname   | dc1.providence.lan   |

| Adresse IP | 192.168.10.15        |

| OS 	     | Windows Server 2016  |

| Domaine    | providence.lan       |

| Rôle       | AD DS, Kerberos, LDAP |



---



\##  Services fournis



\- Active Directory Domain Services

\- Kerberos Authentication

\- LDAP Directory

\- DNS (via serveur01 Linux externe)



---



\##  Sécurité



\- Comptes administrateurs dédiés

\- Séparation utilisateurs / services

\- Stratégies de mot de passe

\- Audit des connexions

\- Journalisation



---



\##  Intégration Linux



Les serveurs Linux sont intégrés via SSSD/Kerberos :



```bash

realm join providence.lan -U Administrateur

authselect select sssd with-mkhomedir



