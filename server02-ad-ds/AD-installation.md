# Installation Active Directory – DC1

## 1- Préparation


- IP statique : 192.168.10.15
- DNS : 192.168.10.10
- Nom du serveur : dc1
---
## 2- Installation du rôle AD DS
Via PowerShell :



```powershell

Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

##3-Promotion en contrôleur de domaine
```powershell
Install-ADDSForest `
-DomainName "providence.lan" `
-DomainNetbiosName "PROVIDENCE"
```

## Verification 
```powershell
dcdiag
Get-ADDomain
```








