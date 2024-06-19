---
tags:
  - PEH
---
## Using Bloodhound
1. To run `Bloodhound`, you must setup and run the `neo4j` console first:
```bash
sudo neo4j console
# Password: neo4j1
```
2. Setup and run `Bloodhound` and sign in using `neo4j` credentials:
```bash
sudo bloodhound
```
3. Now, setup the ingestor related to `bloodhouhnd`:
```bash
bloodhound-python -d <domain-name>.local -u <username> -p <password> -ns <dc-ip-address> -c all
# -u example: fcastle
# -p example: Password of fcastle
# -ns is for name server.
```
4. Upload files to `bloodhound`

>[!TIP] Make a directory
>`bloodhound-python` dumps a lot of files, so it's better to make a directory and cd into it.