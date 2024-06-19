---
tags:
  - PEH
---
## Logical [[Active Directory]] components
### AD DS Schema
Can be thought of as rule book or blue print since it defines every type of object that can be stored in the directory, and it also enforces rules regarding object creation and configuration.

| Object Type      | Function                                            | Examples             |
| ---------------- | --------------------------------------------------- | -------------------- |
| Class Object     | What objects can be created in the active directory | - User<br>- Computer |
| Attribute Object | Information that can be attached to an object       | - Display name       |

### Domains
Domains are used to group and manage objects in an organization. Domains are an administrative boundary for applying policies to groups of objects. 
### Domain trees
Domain trees are hierarchy of domains in AD DS.
### Forests
Forest is a collection of one or more domain trees.
### Organizational units (OU)
Organizational units are AD containers that can contain users, groups, computers, and other OUs.

Organizational units are used to:
- Manage a collection of objects in a consistent way
- Delegate permissions to administer groups of objects
- Apply policies
### Trusts
Trust provides a ==mechanism for users to gain access to resources in **another domain**.==
![[Active Directory Trust.png|center]]
### Objects
Objects live within an organizational unit (OU), and they can be different things:
![[Active Directory Objects.png]]