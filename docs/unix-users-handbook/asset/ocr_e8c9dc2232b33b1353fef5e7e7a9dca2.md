| Phys Wts | The number of physical writes to the disk. This may be due to file system activity or virtual memory management. |
| User | The amount of physical disk I/O as a result of user file I/O operations. |
| Virtual Mem | The amount of physical disk I/O as a result of virtual memory management activity. |
| System | The amount of physical disk I/O as a result of system calls. |
| Raw | The amount of raw mode disk I/O. |

A lot of disk activity may also take place as a result of NFS mounted disks. Statistics are provided for “Remote” disks as well.

Disk access is required on all systems. The question to ask is: What disk activity is unnecessary and slowing down my system? A good place to start is to compare the amount of “User” disk I/O with “Virtual Mem” disk I/O. If your system is performing much more virtual memory I/O than user I/O, you may want to investigate your memory needs.

# GlansePlus Summary

In addition to the Process List, or Global, screen and the CPU, Memory, and Disk screens described earlier, there are many other useful screens including the following:

| Swap Space | Shows details on all swap areas. May be called by another name in other releases. |
| Netwk By Intrfce | Gives details about each LAN card configured on your system. This screen may have another name in other releases. |