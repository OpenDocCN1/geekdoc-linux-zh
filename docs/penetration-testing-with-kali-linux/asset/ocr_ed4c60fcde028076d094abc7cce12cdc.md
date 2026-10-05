# OffSec

Penetration Testing with Kali Linux

We can use a few methods to access the system as user when certain requirements are met. We can use WinRM or RDP to access the system if the user is a member of the corresponding groups. Alternatively, if the target user has the Log on as a batch job right, we can schedule a task to execute a program of this user. Furthermore, if the target user has an active session, we can use PsExec from Sysinternals.

Since we have access to a GUI, we use Runas in PowerShell to start cmd as backupadmin. We will enter the username as /user/ and the command we want to execute. Once we execute the command, password prompt appears which we'll enter the previously found password.

```
PS C:\Users\steve> runas /user:backupadmin cmd
Enter password for backupadmin:
Attempting to start cmd as user "CLIENTWK220\backupadmin" ...nPC:\Users\steve>
```

Listing 396 - Runas to execute cmd as user as backupadmin

Once the password is entered, a new command window appears. The title of the new window starts *running as CLIENTWK220*.
Let's use whoami to confirm the command line is working and we are indeed backupadmin.

![](bbox=[0.185, 0.435, 0.815, 0.8])

Figure 238: Cmd running in the context of backupadmin

Figure 238 shows that we are executing commands as user backupadmin. Very nice!

> 766 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/log-on-as-a-batch-job

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

490