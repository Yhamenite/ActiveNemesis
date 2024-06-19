---
tags:
  - PEH
---
## Methodology
Get account (cracked password or got a NTLM from a relay), Pass Attack and dump secrets, collect, crack, and repeat:
- [[Initial Internal Attack Strategy (AD)|Initial Attack Vectors]]
- [[Post-Compromise Enumeration Strategy|Post-Compromise Enumeration]]
- [[Post-Compromise Attacks Strategy (AD)|Post-Compromise Attacks]]
- [[Post-Domain Compromise Attack Strategy|Post-Domain Compromise Attack]]
![[Flow (Methodology) in attacking AD.png]]
## SUPER IMPORTANT CONSIDERATIONS
- The hash captured from a [[LLMNR Poisoning]] or [[SMB Relay Attacks]] is a NTLMv2 hash. However, the hash dumped from a successful SMB Relay Attack is a NTLMv1 hash (form of LM:NT, the NT part is what we crack). This hash is useful to [[Gaining shell access (in AD)|gain shell access]] and is the one used in [[Pass Attacks]] and is the one that we collect when [[Dumping and cracking hashes|dumping hashes]].
- If the SMB Relay Attack didn't succeed and we didn't find any NTLMv1 hash that we could pass around, we should find a way to crack the NTLMv2 hash and pass it to move laterally and potentially vertically.
- If you have cleartext password and/or NTLMv1 hash, always spray (perform Pass Attacks) using these or one of them
- Whenever you take over an account, make sure to **dump its hashes, collect those hashes, try to break them and/or use them or the password after breaking them in a Pass Attack again and again**
- The methodology above is REPETITIVE AND ITERATIVE