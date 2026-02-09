# Installation du rôle Active Directory (AD DS)

##  Objectif

Mettre en place un contrôleur de domaine Active Directory sur Windows Server afin de fournir une authentification centralisée pour l’infrastructure Linux et Windows.

---

##  Environnement

| Élément | Valeur              |
|-------- |---------------------|
| Serveur | DC1                 |
| OS      | Windows Server 2016 |
| Domaine | providence.lan      |
| Type    | Forêt et domaine racine |

---

## 1. Pré-requis

- Windows Server installé et à jour
- Adresse IP fixe
- DNS configuré vers lui-même
- Nom d’hôte défini (dc1.providence.lan)

---

## 2. Installation du rôle AD DS

Via le **Gestionnaire de serveur** :

1. Ajouter des rôles et fonctionnalités
2. Sélectionner **Services de domaine Active Directory (AD DS)**
3. Inclure les fonctionnalités associées
4. Valider et installer

---

## 3. Promotion en Contrôleur de Domaine

Après l’installation du rôle :

1. Cliquer sur **Promouvoir ce serveur en contrôleur de domaine**
2. Choisir **Ajouter une nouvelle forêt**
3. Nom du domaine : `providence.lan`
4. Niveau fonctionnel : Windows Server 2016
5. Activer :
   - Catalogue global
   !!!!!!! Dans mon cas DNS non integrer a ADDS

---

## 4. Configuration DNS (DNS Linux BIND externe à AD)

Dans mon infrastructure, le DNS **n’est pas hébergé sur Windows Server**.
La résolution est assurée par **server01 (BIND)**, et le contrôleur de domaine
(DC1) dépend de ce DNS externe pour publier et résoudre les enregistrements AD.

### 4.1 Paramètres DNS côté DC (Windows)

Sur le contrôleur de domaine, la carte réseau doit utiliser **uniquement** le DNS Linux :

- DNS primaire : `192.168.10.10` (server01)

Vérification :

```powershell
        ipconfig /all
```
---

## 5. Finalisation

- Redémarrage automatique du serveur
- Vérification des services :
  - AD DS
  - DNS
  - Kerberos
  - Netlogon

Commande de vérification :

```powershell
dcdiag

