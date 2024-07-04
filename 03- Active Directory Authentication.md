
The process of authentication of users and computers to verify their identities to gain access to the network resources in an AD. 

- It plays critical role in ensuring secure access to resources while maintaining centralized control over authentication and access management.
- The most common way for users to authenticate is providing username and password. 

- AD supports the following protocol for authentication
1. Kerberos
2. NTLM


### Kerberos 
Primary authentication protocol used in AD for user authentication. 
##### Features:
- Mutual Authentication: Both the client and server verify each other's identities. 
- Single Sign On (SSO): User authenticate once and can access multiple resources without re-entering credentials. 
- Ticket Based: Authentication exchanges rely on encrypted tickets which reduces the risk of credential theft. 

##### Process:

###### Step #1 :
Client encrypts the current timestamp with a long term key to the Key Distribution Center (KDC). 
##### Step #2:
KDC decrypts the timestamp with user's key that is stored on the AD. If the AD is able to decrypt it and the time is within acceptable range, it will issue a Ticket granting ticket (TGT) to the client. 

##### Step #3:
User receives the TGT and requests for the Ticket  Granting Service (TGS). The request includes the user's TGT (from step 2) and encrypts it with the `krbtgt` account's long term key. 

##### Step #4:
KDC decrypts the TGT and creates a service ticket. The server sends the TGS. 

##### Step #5:
Client receives the service ticket and sends it to the service. 

##### Step #6:
Service verifies it, and grant access of the service to the client. Service may carry some optional steps to verify the service ticket sent by the client. 



### NTLM
An older authentication protocol used by windows system for backward compatibility. 

##### Features:
- **Compatibility**: It is supported by older version of windows system and applications. 
- **Simplicity**: NTLM authentication does not require the complexity of Kerberos, making it easier to implement in certain environment. 
- **Security**: NTLM has limitation compared to Kerberos, including susceptibility to pass-the-hash attack and lack of mutual authentication. 

##### Process:

1. User sends a logon request to DC
2. Server sends a random number as the NTLM challenge
3. User uses that random number and hashes the number with the actual hash of password of the user and sends it to the DC. 
4. Server verifies and give access if authentication is successful. 





