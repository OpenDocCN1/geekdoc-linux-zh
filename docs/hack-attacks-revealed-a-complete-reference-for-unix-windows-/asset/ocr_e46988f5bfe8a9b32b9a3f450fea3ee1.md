![](bbox=[0.12, 0.05, 0.75, 0.38])

**Figure 4.23** The VooDoo Doll feature set.

Doll, have been known to wipe—that is, copy over the target files numerous times, thus making them unrecoverable—entire hard disks, and in some cases corrupt operating system program files.

**Port: 1492**

**Service:** FTP99CMP

**Hacker's Strategy:** FTP99cmp is another simple remote FTP server daemon that uses the following Registry key:

```
HKEY_LOCAL_MACHINE, Software\Microsoft\Windows\CurrentVersion
\Run – WinDLL_16
```

**Port: 1600**

**Service:** Shyvka-Burka

**Hacker's Strategy:** This remote-control Trojan provides simple features, such as file transfer and control, and therefore has been sparsely distributed.

Currently, this daemon does not utilize the system Registry, but is notorious for favoring port 1600.

**Port: 1981**

**Service:** Shockrave

**Hacker's Strategy:** This remote-control daemon is another uncommon telnet stealth suite with only one known compilation that mandates port 1981. During configuration, the following Registry entry is utilized: