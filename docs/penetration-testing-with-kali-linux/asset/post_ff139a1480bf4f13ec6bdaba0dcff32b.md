
```
PS:\Tools> Get-NetSession -ComputerName web04
PS C:\>
```

Listing 756 - Checking logged on users with Get-NetSession

As indicated above, we are not receiving any output. A simple explanation would be that there are no users logged in the machines. However, to make sure we're receiving any error messages, let's use the -Verbose flag:

```
PS:\Tools> Get-NetSession -ComputerName files04 -Verbose
VERBOSE: [Get-NetSession] Error: Access is denied
```

```
PS:\Tools> Get-NetSession -ComputerName web04 -Verbose
VERBOSE: [Get-NetSession] Error: Access is denied
```

Listing 757 - Adding verbosity to our Get-NetSession command

Unfortunately, that NetSessionEnum does not work in this case and returns an "Access is denied" error message. This most likely means that we are not allowed to run the query, and based on the error message, it might have to do with privileges.

Since we may have administrative privileges on CLIENT74 with stephanie, let's run Get-NetSession against that machine and inspect the output there as well:

```
PS:\Tools> Get-NetSession -ComputerName client74
```

| CName : :192.168.50.75 |
| UserName : stephanie |
| Time : 8 |
| IdleTime : 0 |
| ComputerName : client4 |

Listing 758 - Running Get-NetSession on CLIENT74

We received some more information than this. However, looking closer at the output, the IP address in CName (192.168.50.75) does not match the IP address for CLIENT74. In fact, it matches the IP for our current machine, which is CLIENT75. Since we haven't spawned any sessions to CLIENT74, something appears to be off in this case as well.

In a real world, or in the Challenge Labs, we might accept that encountering sessions with PowerView does not work and try a different tool. However, let's use this as a learning opportunity and take a deeper dive into the NetSession API and try to figure out why it does not work in our case.

According to the documentation for NetSessionEnum,¹1036 there are five possible query levels: 0,1,2,10,50. Level 0 only returns the name of the computer establishing the session. Levels 1 and 2 return more but require administrative privileges.

This leaves us with Levels 10 and 50. Both should return information such as the name of the computer and name of the user establishing the connection. By default, PowerView query level 10 with NetSessionEnum, which should give us the information we are interested in.

The permissions required to enumerate sessions with NetSessionEnum are defined in the SrvcInfo registry key, which is located in the

> ¹1036 (Microsoft, 2022), https://learn.microsoft.com/en-us/windows/32/api/lmshare/nf-lmshare-netsessionenum

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Default hive

We use the Windows 11 machine we are currently logged in to check the permissions. Although it may have fewer permissions than the other machines in the environment, it gives us an idea of what is going on.

In order to view the permissions, we use the PowerShell Get-Acl cmdlet. This command will essentially retrieve the permissions for the object we define with the -Path flag and print them in our PowerShell prompt.

```
PS C:\Tools Get-Acl -Path
HKLM:SYSTEM\CurrentControlSet\Services\LanmanServer\Default\ | fl
```

```
Path :
Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Default
Owner : NT AUTHORITY\SYSTEM
Group : NT AUTHORITY\SYSTEM
Access : BUILTIN\Users Read
Administrators Full Control
NT AUTHORITY\SYSTEM Full Control
CREATOR OWNER Full Control
APPLICATION PACKAGE AUTHORITY All ReadKey
S-1-5-32-192-106534681-468-3651178428-1654721687-432734479-32315806-0453264122-345934681 Allow
```

> Listing 759 - Displaying permissions on the DefaultServer registry hive

The highlighted output in Listing 759 reveals the groups and whether they have FullControl or ReadKey, meaning they can all read the SrvcsSessionInfo key.

The long string at the end of the output is, according to Microsoft's documentation, a capability SID. If, the documentation refers to the exact SID in our output

A capability SID is an unforable token of authority that grants a Windows component or a Universal Application access to various resources. However, it will not give us access to the registry key of interest.

In older versions (which Microsoft does not specify), Authenticated Users were allowed to access the registry key and obtain information from the SrvcsSessionInfo key. However, following the least privilege principle, regular domain users should not be able to acquire this information within the domain, which is likely part of the reason for the permissions key has changed. Also, due to permissions, we can be certain that NetSessionEnum will not be able to obtain this type of information on Windows 11.

# OffSec

Penetration Testing with Kali Linux

Now let's get a better sense of the operating system versions use. We can do this with NetComputer, this time including the operatingsystemversion attribute:

```
PS C:\Tools> Get-NetComputer | select
dnhostname,operatingsystemversionoperatingsystemversion
```

| dnhostname | operatingsystem | operatingsystemversion |
|---|---|---|
| DC1.corp.com | Windows Server 2022 | 10.0 (20348) |
| web04.corp.com | Windows Server 2022 | 10.0 (20348) |
| FILES04.corp.com | Windows Server 2022 | 10.0 (20348) |
| client74.corp.com | Windows 11 Pro | 10.0 (22080) |
| client75.corp.com | Windows 10 Pro | 10.0 (22080) |
| CLIENT76.corp.com | Windows 10 Pro | 10.0 (16299) |

Listing 760 - Querying operating system and version

As we discovered, Windows 10 is the oldest operating system in the environment, and based on the output above, this version is 16299, otherwise known as build 1709.${1039}$

While the documentation from Microsoft is not clear when they made a change to the HKEY_LOCAL_MACHINE\CurrentControlSet\Services\LanmanServer\DefaultSecurity registry, it appears to be the release of this exact. It affects Windows Server operating systems since Windows Server 2019 build 1809. This creates an issue since we are not able to use PowerView to build the domain map we had in.

Even though SessionEnum does not work in case, we should still keep it in our toolkit since it's not uncommon to find older systems in real-world environments.

Furthermore there are other tools we can use, such as the PsLogged${1040} application from the SysInternals. The documentation states that PsLogged will enumerate the keys under HKEY_USERS to retrieve the security identifiers (SID) of logged-in users and convert the SIDs to usernames. PsLogged will also use the NetSession API to see who is logged on the computer via resource share.

One limitation, is that PsLogged relies on the Remote Registry service in order to store the associated key. The Remote Registry service has not been enabled by default workstations since Windows 8, but system administrators may enable it for various administrative tasks, for backwards compatibility, or for installing monitoring/deployment tools, scripts, agents, etc.

It is also enabled by default on Windows Server Operating Systems as Server 2012 R2, 2016 (1607), 2019, and Server 2022 (21H2). If it is enabled, the service will stop after ten minutes of inactivity to save resources, and will be re-enable (with an automatic trigger) when we connect with PsLoggedOn.

With the theory out of the way, let's try to run PsLoggedOn against the computers we enumerate starting, using FILES04 and WEB04. PsLoggedOn is located in C:\ToolsPST on CLIENT75. To see, we'll run it with the target host:

> ${1039}$ (Microsoft, 2022), https://learn.microsoft.com/en-us/windows/uwp/whats-new-windows-10-build-16299
${1040}$ (Microsoft, 2021), https://learn.microsoft.com/en-us/sysinternals/downloads/psloggedon
${1041}$ (Microsoft, 2022), https://learn.microsoft.com/en-us/sysinternals/
