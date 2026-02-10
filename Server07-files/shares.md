\# Partages Samba



\## Objectif

Ce document décrit les partages Samba exposés par \*\*server07\*\* et la logique de droits basée sur Active Directory.



---



\##  Partage principal : `Partage`



\- Chemin Linux : `/srv/samba/partage`

\- Accès : utilisateurs du groupe AD `Domain Users`

\- Type : lecture/écriture

\- Permissions : masques UNIX + ACL Windows (via `acl\_xattr`)



\### Configuration Samba



```ini

\[Partage]

&nbsp;  path = /srv/samba/partage

&nbsp;  browseable = yes

&nbsp;  read only = no

&nbsp;  valid users = @"PROVIDENCE\\\\Domain Users"

&nbsp;  force group = "PROVIDENCE\\\\Domain Users"

&nbsp;  create mask = 0660

&nbsp;  directory mask = 2770

```

---

\## Création du répertoire (Linux)

mkdir -p /srv/samba/partage

chown root:"PROVIDENCE\\\\Domain Users" /srv/samba/partage

chmod 2770 /srv/samba/partage



\###Test depuis Windows



Ouvrir : \\\\server07\\Partage

Authentification : PROVIDENCE\\utilisateur



\###Tests de validation (Linux)

```**bash**

testparm -s

wbinfo -t

wbinfo -u | head

wbinfo -g | head

```



