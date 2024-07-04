
### Domains 

Domains are used to group and manage objects in an organization. 
1. An administrative boundary for applying policies to groups of objects. 
2. A replication boundary for replicating data between domain controllers.
3. An authentication and authorization boundary that provides a way to limit the scope of access to resources. 


### Tree
A domain tree is a hierarchy of domain in AD. 

- Share a contiguous namespace with parent domain. 
- Can have additional child domain. 
- By default create a two-way transitive trust with other domains. 


### Forests:

A forest is a collection of one or more trees. 

- Share a common schema.
- Share a common configuration partition. 
- Share a common global catalog to enable searching.
- Enable trusts between all domains in a forest. 
- share the Enterprise Admins and Schema Admins groups. 


### Trusts:

Trusts provides mechanism for users to gain access to resources in another domain. 

1. Directional
	- The trust direction flows from trusting domain to the trusted domain. 
2. Transitive
	1. the trust relationship is extended beyond a two domain trust to include other trusted domains. 

- All domains in a forest trust all other domains in the forest. 
- Trusts can extend outside the forest. 
- Domains can allow access to shared resources outside of their boundaries using a trust. Forest trusts allow users to access resources in any domain in the other forest, as well as logon to any domain in the forest. 

