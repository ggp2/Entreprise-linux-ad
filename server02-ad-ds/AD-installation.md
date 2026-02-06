Document clair, précis et concis, qui résume toute la procédure de jointure Linux au domaine AD WS2016 , avec les étapes, commandes et erreurs rencontrées.





Guide de Jointure d’un Serveur Linux RHEL 9 au Domaine AD WS2016





Domaine AD : providence.lan



Contrôleur de domaine : DC1 (Windows Server 2016)



Serveur Linux : server02 (RHEL 9)



DNS / DHCP : server01 (Linux, 192.168.10.10)



Objectif : permettre à Linux d’utiliser l’authentification AD via SSSD + Kerberos, avec création automatique de home directories.



1\_ Pré-requis



IP fixe pour le serveur Linux dans le LAN



DNS Linux opérationnel et résolvant le FQDN du DC (dc1.providence.lan)



Paquets Linux nécessaires :



dnf install -y realmd sssd krb5-workstation samba-common-tools adcli oddjob oddjob-mkhomedir



2\_ Vérification et correction du nom d’hôte



Erreur rencontrée :



Couldn't join realm: This computer's host name is not set correctly





Solution :



hostnamectl set-hostname server02.providence.lan



Vérification :



hostname

hostname -f



Modifier /etc/hosts pour que le nom corresponde à l’IP :



192.168.10.20  server02.providence.lan server02



3\_ Configuration Kerberos



Erreur rencontrée :



KDC has no support for encryption type





Cause : incompatibilité des types de chiffrement par défaut RHEL 9 / WS2016.



Solution : modifier /etc/krb5.conf :



\[libdefaults]

&nbsp;default\_realm = PROVIDENCE.LAN

&nbsp;dns\_lookup\_realm = false

&nbsp;dns\_lookup\_kdc = true

&nbsp;default\_tkt\_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac

&nbsp;default\_tgs\_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac

&nbsp;permitted\_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 rc4-hmac

&nbsp;forwardable = true

&nbsp;rdns = false



\[realms]

&nbsp;PROVIDENCE.LAN = {

&nbsp;  kdc = dc1.providence.lan

&nbsp;  admin\_server = dc1.providence.lan

&nbsp;}



\[domain\_realm]

&nbsp;.providence.lan = PROVIDENCE.LAN

&nbsp;providence.lan = PROVIDENCE.LAN





Test Kerberos :



kinit Administrateur@PROVIDENCE.LAN

klist





Remarque :



Warning arcfour-hmac used for authentication is deprecated → normal pour WS2016 / labo.



4- Jointure du domaine



Commande :



realm join providence.lan -U Administrateur





Résultat     : silencieux, retour au prompt



Vérification :



realm list

id Administrateur@PROVIDENCE.LAN

getent passwd Administrateur







5️⃣ Configuration SSSD + mkhomedir



Commandes :



authselect select sssd with-mkhomedir

systemctl restart sssd

systemctl enable --now oddjobd.service





oddjobd → création automatique des home directories



Test utilisateur AD :



su - Administrateur@PROVIDENCE.LAN

whoami

pwd





Home directory créé automatiquement



Authentification via AD OK



6- Erreurs rencontrées et corrections

Erreur	Cause	Solution

KDC has no support for encryption type	Types de chiffrement Linux incompatibles avec WS2016	Modifier /etc/krb5.conf pour inclure aes256, aes128 et rc4-hmac



Couldn't join realm: This computer's host name is not set correctly	Nom d’hôte Linux non conforme / non resolvable DNS	hostnamectl set-hostname + modification /etc/hosts

Warning: encryption type arcfour-hmac used is deprecated	RC4 utilisé pour compatibilité WS2016	Warning normal en labo, en production créer un compte AD supportant AES uniquement



&nbsp;Résultat final



Linux server02 est membre du domaine providence.lan



Authentification AD fonctionne via SSSD + Kerberos



Home directories créés automatiquement

