# Procédure d’Intégration au Domaine Active Directory

## 1. Objectif
Intégrer le serveur Linux \*\*server07\*\* au domaine Active Directory

\*\*providence.lan\*\* afin de permettre une authentification centralisée

pour les services Samba.

---
## 2. Prérequis
- Contrôleur de domaine opérationnel
- DNS fonctionnel (server01 – 192.168.10.10)
- Synchronisation NTP avec le DC
- Compte AD disposant des droits d’intégration
- Résolution DNS correcte

Vérification :

ping dc1.providence.lan
host dc1.providence.lan
timedatectl
---
## 3. Installation des Paquets
apt install -y samba winbind krb5-user libpam-winbind libnss-winbind
----
## 4. Configuration Kerberos
```ini
Éditer /etc/krb5.conf

[libdefaults]

&nbsp;default\_realm = PROVIDENCE.LAN
&nbsp;dns\_lookup\_kdc = true
&nbsp;dns\_lookup\_realm = false
&nbsp;test 

kinit Administrateur@PROVIDENCE.LAN
klist
```
----
## 5. Configuration Samba
```Fichier /etc/samba/smb.conf : 
[global]
;workgroup = PROVIDENCE
;realm = PROVIDENCE.LAN
;security = ADS
;winbind use default domain = yes
;kerberos method = secrets and keytab

Validation 
;testparm
```
---
## 6. Jointure au Domaine
net ads join -U Administrateur 

## 6. résultat obtenu sont présenté 

;sont presente sous forme de capture d'écran 

## 7. Tests de Validation

*Trust AD
wbinfo -t
Résultat :
*Utilisateurs et Groupes
wbinfo -u
wbinfo -g
*NSS
getent passwd Administrateur
 
## 8. Validation Finale

Le serveur est considéré comme intégré lorsque :
-Jointure AD réussie
-Winbind actif
-Utilisateurs visibles
-Authentification fonctionnelle
-Accès Samba opérationnel

## 9. Résultat
Le serveur Linux est désormais membre du domaine Active Directory et peut être utilisé comme serveur de fichiers sécurisé.

## 10. Bonnes Pratiques
-Synchroniser l’heure avec le DC
-Sauvegarder smb.conf
-Documenter les changements
-Tester après chaque modification

## NB un fichier de capture d'écran des resultat est mise a disposition pour l'authenticité de travail
