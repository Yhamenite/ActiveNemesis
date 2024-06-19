---
tags:
  - PEH
---
## What is Pass Password/Hash Attacks ?
If we crack a password and/or can dump the SAM hashes, we can leverage both for lateral movements in the network and that is by passing the password/hash to other accounts in the network and check if the user have a successful login in (local admin) anywhere else.
## Using CrackMapExec to execute the attack
### Pass the Password Attack
```bash
crackexecmap smb <network-address/CIDR> -u <user> -d <domain-name>.local -p <password>
```
### Pass the Hash Attack
```bash
crackmapexec smb <network-address/CIDR> -u administrator -H <hash> --local-auth
# Add --sam to dump SAM hashes as you sweep the network and login into devices
# Add --share to enumerate shares
# Add -lsa to dump the local security authority
# Add -M lsassy to run the LSASSY module which has the capability to dump the LSASS
```
>[!INFO] What is LSASS?
>LSASS stands for Local Security Authority Subsystem Service, LSASS is responsible for enforcing the security policy on the system but it does store credentials of the machine.

>LSA secrets are different than LSASS. For example, you can find cleartext passwords, service account passwords, and more in LSA. LSASS is a sub-system of LSA and stores things such as NTLM hashes for domain users, and Kerberos keys/tickets. `-lsa` dumps the LSA secrets and lsassy dumps LSASS. You can also dump LSASS via procdump, task manager, comsvcs, and a few other tooling.
>\- Gray, on TCM Discord server
### The database of CME
Access the database of `CrackMapExec`by using:
```bash
cmedb
# Run help to utilize different options
```
## Pass Attacks mitigations
![[Pass Attacks mitigations.png]]
## Important considerations

>[!INFO] SMB Relay and NTLMv2
>Only NTLMv2 can be relayed (SMB Relay Attack).

>[!INFO] Pass Hash Attack and NTLMv1
>Pass Hash Attack only works with NTLMv1