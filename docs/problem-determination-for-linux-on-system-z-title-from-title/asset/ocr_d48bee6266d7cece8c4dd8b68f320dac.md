```
Mar 25 13:54:34 lnx02 kernel: [<000000000013db4a>] schedule_timeout+0x9e/0x150
Mar 25 13:54:34 lnx02 kernel: [<00000000001b2080>] do_select+0x4a0/0x5e8
Mar 25 13:54:34 lnx02 kernel: [<00000000001b2514>] sys_select+0x34c/0x588
Mar 25 13:54:34 lnx02 kernel: [<00000000001f2ac>] sysc_noemu+0x10/0x16
```

# Table 3-4 SysRq key assignments

| KEY | Operation |
|---|---|
| 'r' | Turns off keyboard raw mode and sets it to XLATE. |
| 'k' | Secure Access Key (SAK) kills all programs on the current virtual console. |
| 'b' | Will immediately reboot the system without syncing or unmounting your disks. |
| 'o' | Will shut your system off. |
| 's' | Will attempt to sync all mounted file systems. |
| 'u' | Will attempt to remount all mounted file systems as read-only. |
| 'p' | Will dump the current registers and flags to your console. |
| 't' | Will dump a list of current tasks and their information to your console. |
| 'm' | Will dump current memory information to your console. |
| 'v' | Dumps the Voyager™ SMP processor information to your console. |
| 'e' | Sends a SIGTERM to all processes, except for init. |
| 'i' | Sends a SIGKILL to all processes, except for init. |
| 'I' | Sends a SIGKILL to all processes, INCLUDING init. |
| '0-8' | Sets the console log level, controlling which kernel messages will be printed to your console. ('0', for example would make it so that only emergency messages like PANICs or OOPSes would make it to your console.) |