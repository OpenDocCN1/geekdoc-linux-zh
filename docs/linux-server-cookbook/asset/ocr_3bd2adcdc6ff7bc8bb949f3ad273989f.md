```
root@ubuntu:~# sar -r 5 2
Linux 5.15.0-43-generic (ubuntu.example.com) 08/13/22 .x86_64. (2 CPU)

19:43:10 kbmemfree kbavail kbbmemused %memused kbbuffers kbcached kbcommit %commit
kbactive kbinact kbdirty
19:43:15 1997052 3476112 211724 5,27 98884 1523420 511164 8,09
787008 905576 0
19:43:20 1997052 3476112 211724 5,27 98884 1523420 511164 8,09
787008 905576 0
Average: 1997052 3476112 211724 5,27 98884 1523420 511164 8,09
787008 905576 0

```

Figure 6.25: Output example for the command sar

# Memory usage for each process

When a process is running, it has three memory values assigned:

+   Virtual memory: It includes all code, data, and shared libraries.
+   Reserved memory: Resident size, the non-swapped physical memory used.
+   Shared memory: The memory shared with other processes
+   

Figure 6.26 shows an excerpt of the top’s output command after pressing M (shift-m) to sort by memory usage:

```
| PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
|282441 qemu 20 0 70,6g 64,2g 12980 S 0,0 25,5 91484:59 qemu-kvm
|281431 qemu 20 0 70,6g 53,4g 13144 S 0,0 21,2 53283:06 qemu-kvm
|281867 qemu 20 0 70,6g 43,1g 13268 S 0,0 17,1 40395:58 qemu-kvm
|91344 qemu 20 0 37,2g 28,6g 13552 S 0,0 11,4 41616:33 qemu-kvm
|89631 qemu 20 0 37,2g 25,3g 13072 S 0,0 10,0 52131:50 qemu-kvm
|91396 qemu 20 0 37,2g 23,3g 13320 S 0,0 9,3 39959:53 qemu-kvm
|83078 qemu 20 0 21,2g 16,0g 10620 S 1,0 6,4 2419:43 qemu-kvm
```

Figure 6.26: Output example for the command sar

The command ps using the long format (aux) shows the usage of the memory of the process. Figure 6.27 shows an example output filtering for a process where VSZ (virtual size) and RSS (resident set size, reserved memory) are displayed in kilobytes:

```
[root@server ~]# ps aux -q 282441
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
qemu 282441 89.1 25.5 74079692 67366884 ? Sl Jun03 91484:59 /usr/libexec/qemu-kvm -name

```

Figure 6.27: Output example for the command ps

The command pmap, with the argument process id, shows an advanced output about the reserved and shared memory.