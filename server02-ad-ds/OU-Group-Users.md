

\# Organisation Active Directory – OU, Groupes et Utilisateurs



\##  Objectif



Structurer Active Directory afin de faciliter :

\- La gestion des utilisateurs

\- L’attribution des droits

\- La délégation administrative

\- L’application des GPO



---



\## 1. Organisation des OU



\### Arborescence proposée

providence.lan

├── OU=Users

├── OU=Groups

├── OU=Servers

│ ├── Linux

│ └── Windows

└── OU=ServiceAccounts





---



\## 2. Gestion des Groupes



\### Types de groupes utilisés



\- Groupes de sécurité

\- Portée : Globale



\### Exemples



| Groupe       | Rôle                        |

|--------------|-----------------------------|

| web-admins   | Administration serveurs web |

| mail-users   | Accès messagerie            |

| vpn-users    | Accès VPN                   |

| linux-admins | Administration serveurs Linux |



---



\## 3. Création des Utilisateurs



Chaque utilisateur est associé à :

\- Une OU dédiée

\- Un ou plusieurs groupes

\- Un UPN cohérent



Exemple :



```powershell

New-ADUser -Name "Alice Mav" -SamAccountName alicemav `

-UserPrincipalName alicemav@providence.lan -Enabled $true



