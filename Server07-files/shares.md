# Partages Samba

## Objectif
Ce document décrit les partages Samba exposés par \*\*server07\*\* et la logique de droits basée sur Active Directory.
---

##  Partage principal : `Partage`

- Chemin Linux : `/srv/samba/partage`
-  Accès : utilisateurs du groupe AD `Domain Users`
-   ype : lecture/écriture
-   Permissions : masques UNIX + ACL Windows (via `acl\_xattr`)

### Configuration Samba

```ini

[Partage]

path = /srv/samba/partage
browseable = yes
read only = no
valid users = @"PROVIDENCE\\\\Domain Users"
force group = "PROVIDENCE\\\\Domain Users"
create mask = 0660
directory mask = 2770

```

---
## Création du répertoire (Linux)

mkdir -p /srv/samba/partage
chown root:"PROVIDENCE\\\\Domain Users" /srv/samba/partage
chmod 2770 /srv/samba/partage

### Test depuis Windows

Ouvrir : \\\\server07\\Partage
Authentification : PROVIDENCE\\utilisateur

### Tests de validation (Linux)

```**bash
testparm -s
wbinfo -t
wbinfo -u | head
wbinfo -g | head

```



