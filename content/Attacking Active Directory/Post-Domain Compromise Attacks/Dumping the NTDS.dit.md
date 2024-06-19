---
tags:
  - PEH
---
## Definition of NTDS.dit
NTDS.dit is a **database used to store Active Directory data**. This data includes;
- User information
- Group information
- Security descriptors
- Password hashes
>[!INFO] NTDS.dit
>NTDS.dit stands for "New Technology Directory Service Directory Information Tree"
## Dumping the NTDS.dit

>[!SUCCESS] DC hashes
>Remember that you can dump the Domain Controller (DC) hashes by using the secretsdump of a compromised **user in the "Domain Admin (DA)" group** and pointing the IP address to the DC.

1. Dump the hashes of the DC (the following command is the same command used in [[Token Impersonation]] Attack, but the added flag only dumps the NTDS.dit)
```bash
secretsdump.py <domain-name>/<DA-user>:"<password>"@<dc-ip> -just-dc-ntlm
```
2. Filter out the data using Excel. Paste the hashes `->` Data, Text to Columns `->` Set a delimiter of ":" `->` Deleted the RID and the LM part of the hash
3. Crack the hashes
4. Paste the results in a new tab (the results are Hash : Cracked Hash)
5. Now make a VLOOKUP function and most importantly change the passwords column to text