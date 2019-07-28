---
title: Automating Role-Based AD Security Groups
thumbnail: /assets/images/automate-adsg.png
category: automation
tags: 'powershell, active-directory, security-groups'
---
![](https://github.com/infamousjoeg/joeco.de/blob/gh-pages/assets/images/automate-adsg.png?raw=true)

When I create a new Safe in CyberArk PAS, I always create three (3) role-based security groups in Active Directory that segregates the duties I need in each safe.  I create an Admin security group, Auditors security group, and Users security group - each with different permissions.

Creating these security groups in Active Directory can take some time.  Also, it's an easily repeatable process - so, it's a good candidate for some AUTOMATION!

In this quick little PowerShell script I wrote, I ask the user running the script to provide the Safe Name since that is the backbone of my security group's naming convention.  After that, each of the three security groups are created and then it's up to me to populate the members from there.

Hope this helps someone out there!

```powershell
Import-Module ActiveDirectory

$safeName = Read-Host "Enter the name of the safe in CyberArk PAS"

Write-Output "Creating security group ${safeName}_Admin"
New-ADGroup -Name "${safeName}_Admin" -SamAccountName "${safeName}_Admin" `
    -GroupCategory Security -GroupScope Global -DisplayName "${safeName}_Admin" `
    -Path "OU=Security Groups,OU=Groups,DC=cybr,DC=dev" `
    -Description "Members of this group are ${safeName} Safe Administrators"

Write-Output "Creating security group ${safeName}_Auditors"
New-ADGroup -Name "${safeName}_Auditors" -SamAccountName "${safeName}_Auditors" `
    -GroupCategory Security -GroupScope Global -DisplayName "${safeName}_Auditors" `
    -Path "OU=Security Groups,OU=Groups,DC=cybr,DC=dev" `
    -Description "Members of this group are ${safeName} Safe Auditors"

Write-Output "Creating security group ${safeName}_Users"
New-ADGroup -Name "${safeName}_Users" -SamAccountName "${safeName}_Users" `
    -GroupCategory Security -GroupScope Global -DisplayName "${safeName}_Users" `
    -Path "OU=Security Groups,OU=Groups,DC=cybr,DC=dev" `
    -Description "Members of this group are ${safeName} Safe Users"

Write-Output "Process completed."
```
