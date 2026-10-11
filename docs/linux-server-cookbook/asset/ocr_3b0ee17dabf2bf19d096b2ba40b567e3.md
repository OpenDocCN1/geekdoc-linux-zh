```
[root@server ~]# lscpu|grep --color=never -E "^(CPU\(|Thread|Core|Socket|NUMA)" CPU(s): 32 Thread(s) per core: 2 Core(s) per socket: 8 Socket(s): 2 NUMA node(s): 2 NUMA node0 CPU(s): 0-7,16-23 NUMA node1 CPU(s): 8-15,24-31
```

*Figure 6.2: Using command lscpu to obtain CPU information.*

The command **lstopo-no-graphics** part of the package **hwloc** provides a great visualization of the NUMA architecture and the association between CPUs and local memory. *Figure 6.3* illustrates an output example of this command for the same server as *figure 6.2*:

![](bbox=[0.13, 0.37, 0.87, 0.63])

*Figure 6.3: Output example for the command lstopo-no-graphics.*

The file `/proc/cpuinfo` contains the list of all processors (*core/thread*) with a detailed information for each one. *Figure 6.4* shows an example using **grep**, **sort**, and **uniq** to create a report of how many CPUs are in each socket:

```
[root@server ~]# grep "physical id" /proc/cpuinfo |sort|uniq -c 16 physical id : 0 16 physical id : 1
```

*Figure 6.4: Getting information from file /proc/cpuinfo*

Other example commands to get processor information are as follows:

+   - *lshw -class processor* (*lshw -class processor -short*)