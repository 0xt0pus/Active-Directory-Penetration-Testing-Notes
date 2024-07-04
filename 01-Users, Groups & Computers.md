
### Domain Users

- Users represent individuals who interact with the network. Each user has a unique account within active directory identified by a username and associated password. 
- User account in AD stores info such as Full Name, Email Address, Phone number, Job title and department. This can be used for authentication, authorization and management process.
- Administrators can manage these user accounts using management tools. 

### Groups

Collection of user accounts, computer accounts and other groups in AD. They provides convenient way to manage access permissions and apply security settings to multiple users or computers. 

##### Two Types of Groups

#### 1. Security Groups
- Used to manage access permission to network resources. Users can be added to security groups and permissions can be assigned to these groups to control resources access. 
#### 2. Distribution Groups
- Used for sending email messages to a group of recipients. 

The following are the **Security Groups** in AD. 

1. Domain Admins
	- Most powerful security group in AD 
	- Created when the domain is first installed
	- Has full administrative control over the entire domain. 

2. Enterprise Admins
	- Forest-wide security group that holds administrative privileges over all domains within a forest. 
	
3. Server Operators
	-  Security group with permission to manage domain controllers and member servers within the domain. 
	
4. Backup Operator
	- Security group with permission to backup and restore operations on DC and member servers. 
5. Account Operators
	- Security group with permission to manage user accounts, groups and computer accounts within a domain.
6. Domain Users
	-  Individual accounts created within the AD to represent people who interact with the network. 
7. Domain Computers
	- Devices including workstations, laptops, servers and other networked devices that are joined to the AD. When computer joins the domain, it establishes a trust relationship with the domain and becomes a member of the domain. 
8. Domain Controllers
	- DC is server that operates within AD and responsible for authenticating users, authorizing access to resources and maintaining the directory database. 


### Computers

- Physical or virtual devices that are joined to the AD including workstations, laptops, servers and other network devices. 
- Each computer within the domain identified by a unique name. When computer joins the domain, a secure trust relationship is established bw the computer and the domain. Which allows the computers to authenticate users and access network resources. 
- Computers accounts in AD stores info such as computer name, OS version and last login time etc. These computers can be managed by administrators using AD management tools. 

