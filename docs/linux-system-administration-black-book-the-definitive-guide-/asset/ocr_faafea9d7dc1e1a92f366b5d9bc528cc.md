+   4. Uncomment this code by placing the cursor over each semicolon and then typing “x”. You should end up with the following:

```
[netlogon]

    comment = Network Logon Service
    path = /home/netlogon
    guest ok = yes
    writable = no
    share modes = no
```

+   5. Do not change the share’s name, because [netlogon] is a reserved share that tells Samba that you want to activate the Windows NT Netlogon service. It is safe, however, to change the other share definition options. If you want to do this, edit them now.

+   6. Press the Esc key to make sure you are in Command mode, and then type “1G” to jump to the beginning of the file.

+   7. Type “/logon script” and press Enter to search down to the following code:

```
#if you enable domain logons then you may want a per-machine or
#per user logon script
#run a specific logon batch file per workstation (machine)
; logon script = %m.bat
#run a specific logon batch file per username
; logon script = %U.bat
```

+   8. It is best to start with a generic logon script and use it for testing; then, when you are sure that it works in general, you can break it into more complex, specialized scripts. Start by adding the following line:

```
logon script = test.bat
```

> **NOTE:** The .bat extension is for scripts for Windows 95 and 98 machines, whereas .cmd is for Windows NT machines.

+   9. Press the Esc key, and then type “ZZ” to save and close the file. Do not restart the Samba server yet, because the files are not in place.

+   10. Create your batch or command file(s) on a Windows machine, if you can. This avoids any discrepancies between how a Linux machine handles characters such as the Enter key and how a Windows machine handles them. Because batch and command file programming for Windows