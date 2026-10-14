# Figure 14.8 sar interactive session on HPUX 10.20.

# Free

The free command is included in the Red Hat Linux 6.0 distribution.

The free command displays the amount of memory in a system. It provides you with a breakdown of total, used, and free memory statistics for physical and swap memory. The command free -o -t produces:

| total | used | free | shared | buffers | cached |
| Mem: | 28976 | 25976 | 264000 | 5780 | 4892 | 12528 |
| Swap: | 265032 | 8992 | 256040 |  |  |  |
| Total: | 555008 | 34968 | 520040 |  |  |  |

free can be run continuously with the -s switch.

free-Displays the amount of memory. It is available in Red Hat Linux 6.0.

# top

top is a great utility to identify processes consuming large percentages of processor time. Figure 14.9 depicts the output from an HPUX 10.20 system. The header gives you an overview of the number of processes run-

![](bbox=[0.045, 0.15, 0.875, 0.65])