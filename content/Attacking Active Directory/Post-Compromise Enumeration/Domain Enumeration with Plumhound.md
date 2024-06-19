---
tags:
  - PEH
---
## Using Plumhound
1. `Plumhound` fetches all its information from `bloodhound`, and `bloodhound` requires `neo4j` to be up and running. So first, do all of the steps in the [[Domain Enumeration with Bloodhound]] document
2. Test to see if the previous steps were applied correctly or not:
```bash
# After accessing /opt/plumhound
sudo python3 plumhound.py --easy -p <neo4j-passowrd>
```
3. If the tests were successful, we can now proceed to run `plumhound`:
```bash
sudo python3 plumhound.py -x <task> -p <neo4j-password>
# <task> is usually tasks/default.tasks
```
4. cd into the reports directory and run `firefox` to view the `index.html` file:
```bash
firefox index.html
```