| Capability ID | Capability Name | Meaning | Status in /etc/lids/lids.cap |
|---|---|---|---|
| 23 | CAP_SYS_NICE | Allow/disallow changing of process priority using the *nice* command. | Allow |
| 24 | CAP_SYS_RESOURCE | Allow/disallow setting of system resource limit | Allow |
| 25 | CAP_SYS_TIME | Allow/disallow setting of system time | Allow |
| 26 | CAP_SYS_TTY_CONFIG | Allow/disallow pseudo-terminal (TTY) configuration | Allow |
| 27 | CAP_MKNOD | Allow/disallow the privileged aspects of *mknod*() system call. | Allow |
| 28 | CAP_LEASE | Allow/disallow taking of leases on files | Allow |
| 29 | CAP_HIDDEN | Allow/disallow hiding of a process from rest of the system | Allow |
| 30 | CAP_INIT_KILL | Allow/disallow programs the capability of killing children of the *init* process (PID = 1) | Allow |

The default settings for the above Linux Capabilities are stored in */etc/lids/lids.cap* file as shown in Listing 23-8.

# Listing 23-8: */etc/lids/lids.cap*

```
+0:CAP_CHOWN
+1:CAP_DAC_OVERRIDE
+2:CAP_DAC_READ_SEARCH
+3:CAP_FOWNER
+4:CAP_FSETID
+5:CAP_KILL
+6:CAP_SETGID
+7:CAP_SETUID
+8:CAP_SETPCAP
-9:CAP_LINUX_IMMUTABLE
```