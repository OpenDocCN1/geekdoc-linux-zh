```
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc0.d
drwxr-xr-x   2 root     root       4096 Oct 21 13:42 rc1.d
drwxr-xr-x   2 root     root       4096 Oct 22 15:40 rc2.d
drwxr-xr-x   2 root     root       4096 Oct 22 15:40 rc3.d
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc4.d
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc5.d
drwxr-xr-x   2 root     root       4096 Jul 29 14:30 rc6.d
drwxr-xr-x   2 root     root       4096 Oct 21 13:41 rcS.d
```

Each of these directories contains scripts to be executed when the system enters a particular runlevel (0–6 and S). Table 4.1 shows the significance of each runlevel. The system's init process (always the first process to be executed) invokes the actions found in the `/etc/init`tab file, which in turn, invokes the appropriate file in `/etc/rc.d` as the system enters each runlevel.

# Table 4.1        The Linux Runlevels and Their Meanings

| Runlevel | Meaning | 
| :--- | :--- | 
| 0 | Halt the system (shutdown) | 
| 1 | Multi-user mode without network | 
| 2 | Multi-user mode with network | 
| 3 | Multi-user mode with network and xdm (X-display manager) | 
| 4 | Reserved (not used by Linux) | 
| 5 | Reserved (not used by Linux) | 
| 6 | System restart (reboot) | 
| S | Single-user mode |

Each directory contains both start scripts (filename starts with S) and kill scripts (filename starts with K), as shown in Listing 4.4.