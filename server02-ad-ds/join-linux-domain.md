# Jointure d’un Serveur Linux RHEL 9 au Domaine Active Directory

##  Objectif

Ce document décrit la procédure complète permettant d’intégrer un serveur
Linux RHEL 9 au domaine Active Directory **providence.lan** afin d’assurer
une authentification centralisée via SSSD et Kerberos.

---

##  Environnement

| Élément       | Valeur                    |
|---------------|---------------------------|
| Domaine AD    | providence.lan            |
| Contrôleur    | DC1 (Windows Server 2016) |
| Serveur Linux | server0 (RHEL 9)         |
| DNS/DHCP      | server01 (192.168.10.10)  |

---

## 1. Prérequis

- Adresse IP fixe
- Résolution DNS fonctionnelle
- Accès au contrôleur de domaine
- Droits administrateur AD

### Installation des paquets

```bash
dnf install -y realmd sssd krb5-workstation \
samba-common-tools adcli oddjob oddjob-mkhomedir
```
---
## 2. Configuration du Nom d’Hôte
Erreur rencontrée
Couldn't join realm: This computer's host name is not set correctly

Correction
```bash hostnamectl set-hostname server02.providence.lan ```

Vérification :
```bash
 hostname
 hostname -f
```
Modifier /etc/hosts :

192.168.10.20   server02.providence.lan   server02
---
## 3. Configuration Kerberos
Problème
```bash KDC has no support for encryption type ```
Cause
Incompatibilité RHEL 9 / Windows Server 2016.

 Correction /etc/krb5.conf
```bash 
[libdefaults]
 default_realm = PROVIDENCE.LAN
 dns_lookup_realm = false
 dns_lookup_kdc = true
 default_tkt_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac
 default_tgs_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac
 permitted_enctypes   = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac
 forwardable = true
 rdns = false

[realms]
 PROVIDENCE.LAN = {
  kdc = dc1.providence.lan
  admin_server = dc1.providence.lan
 }

[domain_realm]
 .providence.lan = PROVIDENCE.LAN
 providence.lan = PROVIDENCE.LAN
```
Test Kerberos
 ```bash
     kinit Administrateur@PROVIDENCE.LAN
     klist
```
---
## 4. Jointure au Domaine
```bash 
realm join providence.lan -U Administrateur
```

Vérification
```bash
realm list
id Administrateur@PROVIDENCE.LAN
getent passwd Administrateur
```
---
## 5. Configuration SSSD et Home Directo
```bash
authselect select sssd with-mkhomedir
systemctl restart sssd
systemctl enable --now oddjobd.service
```
## 6. Test Utilisateur AD
```bash
su - Administrateur@PROVIDENCE.LAN
whoami
pwd
```
## 7. Problèmes Rencontrés

| Problème        | Cause                    | Solution               |
| --------------- | ------------------------ | ---------------------- |
| Erreur Kerberos | Chiffrement incompatible | Modification krb5.conf |
| Join refusé     | Hostname incorrect       | hostnamectl + hosts    |
| Warning RC4     | WS2016 ancien            | Toléré en labo         |

## 8. Résultat Final
- Serveur membre du domaine
- Authentification centralisée
- SSSD opérationnel
- Kerberos fonctionnel

## 9. Bonnes Pratiques
- Synchroniser l’heure avec le DC 
- Sauvegarder les fichiers système
- Tester après chaque modification


