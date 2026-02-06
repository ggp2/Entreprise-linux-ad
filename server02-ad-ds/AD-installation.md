---

:



```markdown

\\# Installation Active Directory – DC1



\\## 1- Préparation



\\- IP statique : 192.168.10.15

\\- DNS : 192.168.10.10

\\- Nom du serveur : dc1



---



\\## 2- Installation du rôle AD DS



Via PowerShell :



```powershell

Install-WindowsFeature AD-Domain-Services -IncludeManagementTools



##3-Promotion en contrôleur de domaine

Install-ADDSForest `

\&nbsp;-DomainName "providence.lan" `

\&nbsp;-DomainNetbiosName "PROVIDENCE"



\## Verification 

dcdiag

Get-ADDomain








