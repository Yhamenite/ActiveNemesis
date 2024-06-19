---
tags:
  - PEH
---
## What is Passback Attacks?
Passback attack happens when you hack into a printer or any IoT device (usually through normal credentials) and change the LDAP(S) from the domain controller (DC) to your IP address. Afterwards the traffic will most-likely show password in plaintext and it can be captured using `responder` or `netcat`. [Very useful article and walkthrough](https://www.mindpointgroup.com/blog/how-to-hack-through-a-pass-back-attack)