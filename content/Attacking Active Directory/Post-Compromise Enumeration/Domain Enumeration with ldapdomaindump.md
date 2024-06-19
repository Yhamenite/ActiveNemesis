---
tags:
  - PEH
---
## Using ldapdomaindump
1. Use ldapdomaindump from /usr/bin
```bash
sudo /usr/bin/ldapdomaindump ldaps://<domain-controller-ip> -u "<domain\user>" -p "<password>"
```

>[!TIP] Make a directory
>`ldampdomaindump` dumps a lot of files, so it's better to make a directory and cd into it.