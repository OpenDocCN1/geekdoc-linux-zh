| Table 16.2 — The Proc Tools (continued) |  |
|---|---|
| **Command** | **Purpose** |
| `psig` | Lists signal actions |
| `pstack` | Displays a stack trace |
| `pstop` | Stops the process |
| `ptime` | Displays the time of process execution |
| `ptree` | Displays the process tree (process and any child processes) |
| `pwait` | Waits for the process to terminate |
| `pwdx` | Displays the current working directory |

The following listing shows sample usage of some of the proc tools. They are used to examine the process (PID = 763) created by the vi /etc/passwd command executed by the da user account (UID = 1001 and GID = 10). The system was accessed remotely from the “wint40” system using an X window terminal. The user is currently located under the d1a home directory (/export/home/d1a):

```
```text
$ pflags 763
763:    vi /etc/passwd
        data model = ILP32  flags = PR_ORPHAN
    /1:    flags = PR_PRCINVAL,PR_ASLEEP [ read(0x0,0x8045d47,0x1) ]

$ pcred 763
763:    e/r/suid=1001  e/r/sgid=10

$ pfiles 763
763:   vi /etc/passwd
    Current rlimit: 256 file descriptors
        0: S_IFCHR mode:0620 dev:102,0 ino:429381 uid:1001 gid:7
           0_RDWR
        1: S_IFCHR mode:0620 dev:102,0 ino:429381 uid:1001 gid:7
           0_RDWR
        2: S_IFCHR mode:0620 dev:102,0 ino:429381 uid:1001 gid:7
           0_RDWR
        3: S_IFCHR mode:0666 dev:102,0 ino:429338 uid:0 gid:3
           0_RDWR
        4: S_IFREG mode:0600 dev:102,0 ino:880803 uid:1001 gid:10
           0_RDWR
        6: S_IFCHR mode:0620 dev:102,0 ino:429381 uid:1001 gid:7
           0_RDWR

$ ptree 763
  759   /usr/openwin/bin/xterm -display winit40:0
  760     sh
    763   vi /etc/passwd
  $

$ pwdx 763
763:    /export/home/d1a
$ 
```
```