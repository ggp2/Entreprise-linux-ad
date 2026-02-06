Document clair, précis et concis, qui résume toute la procédure de jointure Linux au domaine AD WS2016 , avec les étapes, commandes et erreurs rencontrées.

Guide de Jointure d'un Serveur Linux RHEL 9 au Domaine AD WS2016

Domaine AD : providence.lan

Contrôleur de domaine : DC1 (Windows Server 2016)

Serveur Linux : serveur02 (RHEL 9)

DNS / DHCP : server01 (Linux, 192.168.10.10)

Objectif : permettre à Linux d'utiliser l'authentification AD via SSSD + Kerberos, avec création automatique de répertoires personnels.

1_ Prérequis

IP fixe pour le serveur Linux dans le LAN

DNS Linux opérationnel et résolvant le FQDN du DC (dc1.providence.lan)

Paquets Linux nécessaires :

dnf install -y realmd sssd krb5-workstation samba-common-tools adcli oddjob oddjob-mkhomedir

2_ Vérification et correction du nom d'hôte

Erreur rencontrée :

Impossible de rejoindre le domaine : le nom d'hôte de cet ordinateur n'est pas correctement configuré.

Solution :

hostnamectl set-hostname server02.providence.lan

Vérification :

nom d'hôte

nom d'hôte -f

Modifier /etc/hosts pour que le nom corresponde à l'IP :

192.168.10.20 server02.providence.lan server02

3_ Configuration Kerberos

Erreur rencontrée :

KDC ne prend pas en charge le type de chiffrement

Cause : incompatibilité des types de chiffrement par défaut RHEL 9 / WS2016.

Solution : modifier /etc/krb5.conf :

[libdefaults]

 default_realm = PROVIDENCE.LAN

 dns_lookup_realm = faux

 dns_lookup_kdc = vrai

 default_tkt_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac

 default_tgs_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac

 types_enc autorisés = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac

 transférable = vrai

 rdns = faux

[royaumes]

 PROVIDENCE.LAN = {

  kdc = dc1.providence.lan

  serveur_admin = dc1.providence.lan

 }

[domaine_realm]

 .providence.lan = PROVIDENCE.LAN

 providence.lan = PROVIDENCE.LAN

Test Kerberos :

kinit Administrateur@PROVIDENCE.LAN

klist

Remarque :

Avertissement : arcfour-hmac utilisé pour l’authentification est obsolète → normal pour WS2016 / labo.

4- Jointure du domaine

Commande :

realm join providence.lan -U Administrateur

Résultat : silencieux, retour au prompt

Vérification :

liste des royaumes

id Administrateur@PROVIDENCE.LAN

getent passwd Administrateur

5️⃣ Configuration SSSD + mkhomedir

Commandes :

authselect select sssd with-mkhomedir

systemctl restart sssd

systemctl enable --now oddjobd.service

oddjobd → création automatique des répertoires personnels

Test utilisateur AD :

su - Administrateur@PROVIDENCE.LAN

qui suis-je

mot de passe

Répertoire personnel créé automatiquement

Authentification via AD OK

6- Erreurs rencontrées et corrections

Erreur Cause Solution

KDC ne prend pas en charge le type de chiffrement Types de chiffrement Linux incompatibles avec WS2016 Modifier /etc/krb5.conf pour inclure aes256, aes128 et rc4-hmac

Impossible de rejoindre le domaine : le nom d'hôte de cet ordinateur n'est pas correctement configuré. Nom d'hôte Linux non conforme / DNS non résolvable. hostnamectl set-hostname + modification /etc/hosts

Attention : le type de chiffrement arcfour-hmac utilisé est obsolète RC4 utilisé pour compatibilité WS2016 Attention normal en labo, en production créer un compte AD supportant AES uniquement

 Résultat final

Linux server02 est membre du domaine providence.lan

L'authentification AD fonctionne via SSSD + Kerberos

Les répertoires personnels sont créés automatiquement