specifying the delay in seconds between each update (keeping in mind that the top tool may provide a better way to view this data in real time):

```
$ free -s 1
Mem:         3823720      879472     1561532     226220     1382716     2476744
Swap:        2097148           0     2097148

               total       used       free     shared buff/cache   available
Mem:         3823720      879140     1559940     228144     1384640     2475152
Swap:        2097148           0     2097148
.
.
```

To monitor disk I/O from the command line, consider using the iotop command, which can be installed as follows:

```
# dnf install iotop
```

Once installed and executed (iotop must be run with system administrator privileges), the tool will display a real-time list of disk I/O on a per-process basis:

![](bbox=[0.26, 0.48, 0.78, 0.7])

Figure 34-8

# 34.4 Summary

Even a system that appears to be doing nothing will have many system processes running in the background. Activities performed by users on the system will result in additional processes being started. Processes can also spawn their own child processes. Each process will use some system resources, including memory, swap space, processor cycles, disk storage, and network bandwidth. This chapter has explored a set of tools that can be used to monitor both process and system resources on a running system and, when necessary, kill errant processes that may be impacting the performance of a system.