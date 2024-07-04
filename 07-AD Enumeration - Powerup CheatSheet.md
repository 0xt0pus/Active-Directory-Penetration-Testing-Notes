
```powershell
powershell -ep bypass
```

```powershell
. .\powerview.ps1
```


Get Current Domain:
```powershell
Get-Domain
```

Get Information about the parent Domain:
```powershell
Get-Domain -Domain SECURITY.local
```

Get Domain SID:
```powershell
Get-DomainSID
```


Get the Domain Policy:
```powershell
Get-DomainPolicy

(Get-DomainPolicy)."SystemAccess"
(Get-DomainPolicy)."kerberospolicy"
```


Get Information about the domain controller:

```powershell
Get-DomainController
```

```powershell
Get-DomainController -Domain SECURITY.local
```


User Enumeration:
```powershell
Get-DomainUser

Get-DomainUser | select samaccountname, objects
```


Get details of specific user:
```powershell
Get-DomainUser -Identity USERNAME


Get-DomainUser -Identity USERNAME -Properties DisplayName,MemberOf,Objectsid,useraccountcontrol
```


Enumerate Domain Computers:

```powershell
Get-NetComputer

Get-NetComputer -Domain SECURITY.local
Get-NetComputer | select name
Get-NetComputer | select name,cn,operatingsystem
```


Enumerate Groups:
```powershell
Get-NetGroup
Get-NetGroup | select name
```

Get the info about the Domain Admins group:
```powershell
Get-NetGroup 'Domain Admins'
```


Find the members of the group:
```powershell
Get-NetGroupMember "Domain Admins" | select MemberName
```


A user member of which groups?:

```powershell
Get-NetGroup -userName "USERNAME" | select name
```



Enumerate the Domain Shares:
```powershell
Find-DomainShare -ComputerName prod.research.SECURITY.local -verbose
```


The shares for which the current user has read access to?

```powershell
Find-DomainShare -ComputerName prod.research.SECURITY.local -CheckShareAccess -verbose
```


Find the Group Policy Objects (GPOs):
```powershell
Get-NetGRP | select displayname
```


Get the organizational Units:
```powershell
Get-NetOU

Get-NetOU | select name
```


Get Trust:
```powershell
Get-NetDomainTrust
```

Get Forest:
```powershell
Get-NetForest
```

Map the trust of forest:
```powershell
Get-NetForestTrust
```


```powershell
Get-NetForestTrust -Forest tech.local
```


```powershell
Get-NetForest -Forest tech.local
```

So, the trust is established. Now we can start enumerating the other domain. 


Get the all the domains in the current forests:
```powershell
Get-NetForestDomain
```

Check Domains in the other forest:
```powershell
Get-NetForestDomain -Forest OtherDomain.local
```


Check the mapping:
```powershell
Get-DomaintrustMapping
```

#### ACLs
ACLs used to regulate access to resources. 

  
```powershell
Get-ObjectAcl -SamAccountName "users" -ResolveGUIDs
```

Find interesting ACLS:

```powershell
Find-InterestingDomainAcl -ResolveGUIDs
```


Finding Kerberoastable Accounts:

```powershell
Get-NetUser -sPN | select samaccountname,serviceprincipalname
```


Find AREP Roastable accounts:
```powershell
Get-NetUser -PreauthNotRequired select samaccountname,useraccountcontrol
```
