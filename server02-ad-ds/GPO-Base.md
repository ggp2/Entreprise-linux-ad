\# Gestion des Stratégies de Groupe (GPO)



\##  Objectif



Ce document présente la mise en place et l’utilisation des GPO dans le domaine providence.lan afin de renforcer la sécurité, standardiser les postes et centraliser l’administration.



---



\## 1. Rôle des GPO



Les stratégies de groupe permettent de :



\- Appliquer des règles de sécurité

\- Configurer les postes automatiquement

\- Restreindre les utilisateurs

\- Déployer des scripts

\- Gérer les accès réseau



---



\## 2. Organisation des GPO



Les GPO sont liées aux OU suivantes :



OU=Users

OU=Servers

OU=Computers

OU=Admins





Chaque OU possède ses propres stratégies.



---



\## 3. GPO de Sécurité



\### 3.1 Politique des mots de passe



\- Longueur minimale : 10 caractères

\- Historique : 5 mots de passe

\- Expiration : 90 jours

\- Complexité activée



---



\### 3.2 Verrouillage de session



\- Verrouillage après 5 échecs

\- Déverrouillage après 15 minutes



---



\### 3.3 Pare-feu Windows



\- Pare-feu activé

\- Blocage connexions entrantes

\- RDP autorisé uniquement aux admins



---



\## 4. GPO Utilisateurs



\### Restrictions



\- Accès panneau de configuration limité

\- Désactivation du CMD pour utilisateurs

\- Interdiction modification réseau



---



\### Redirection dossiers



\- Documents → Serveur fichiers

\- Bureau → Serveur fichiers



---



\## 5. Mapping des lecteurs réseau



Exemple :



| Lecteur | Partage            |

|---------|--------------------|

| Z:      | \\\\server04\\partage |

| Y:      | \\\\server04\\users   |



Déploiement via GPO Preferences.



---



\## 6. Scripts de connexion



Scripts PowerShell exécutés au login :



\- Mapping réseau

\- Nettoyage dossiers temporaires

\- Synchronisation



---



\## 7. Vérification



Commandes :



```powershell

gpresult /r

rsop.msc



---

\##8. Bonnes Pratiques



-Une GPO = un objectif



-Nom clair



-Documentation



-Tests avant production



-Sauvegarde GPO

---



\##9. Résultat



Postes sécurisés



Configuration centralisée



Réduction des erreurs humaines



Administration simplifiée

