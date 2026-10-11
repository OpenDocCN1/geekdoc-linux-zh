Sysinternals – www.sysinternals.com

```
C:\Windows\system32> **ipconfig**

Windows IP Configuration

Ethernet adapter Ethernet0:

Connection-specific DNS Suffix . . : 
Link-local IPv6 Address . . . . . . . : fe80::7959:aaad:eec:3969%2
IPv4 Address. . . . . . . . . . . . . : 192.168.1.110
Subnet Mask . . . . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . . . : 192.168.1.1
...
```

```
C:\Windows\system32> **whoam /fakeuser**
corp\fakeuser

C:\Windows\system32> **whoam /groups**

GROUP INFORMATION
-----------------
Group Name            Type          Attributes
============          ====          ============================
Everyone              Well-known group Mandatory group, Enabled by default
BUILTIN\Administrators Alias        Mandatory group, Enabled by default
BUILTIN\Users         Alias         Mandatory group, Enabled by default
...
NT AUTHORITY\Authenticated Users Well-known group Mandatory group, Enabled by default
NT AUTHORITY\This Organization Well-known group Mandatory group, Enabled by default
CORP\**Domain Admins**   Group         Mandatory group, Enabled by default
CORP\Group Policy Creator Owners Group     Mandatory group, Enabled by default
CORP\Schema Admins      Group        Mandatory group, Enabled by default
CORP\Enterprise Admins   Group         Mandatory group, Enabled by default
...
Mandatory Label\High Mandatory Level Label
```

*Listing 726 - Performing lateral movement using the golden ticket and PsExec*

We have an interactive command prompt on the domain controller and notice that the **whoam** command reports us to be the user fakeuser, which does not exist in the domain. Listing group memberships shows that we are a member of multiple powerful groups including the Domain Admins group. Excellent.

> *The use of a non-existent username may alert incident handlers if they are reviewing access logs. In order to reduce suspicion, consider using the name and ID of an existing system administrator.*

Note that by creating our own TGT and then using PsExec, we are performing the overpass the hash attack by leveraging Kerberos authentication. If we were to connect using PsExec to the IP