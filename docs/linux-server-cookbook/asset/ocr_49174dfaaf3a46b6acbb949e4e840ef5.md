```
0[0.7%] 4[0.0%] 8[0.0%] 12[6.0%] 16[0.0%] 20[0.0%] 24[0.0%] 28[0.0%]
1[0.7%] 5[0.7%] 9[0.0%] 13[0.0%] 17[0.0%] 21[0.7%] 25[0.0%] 29[0.0%]
2[0.7%] 6[0.0%] 10[0.0%] 14[0.0%] 18[0.7%] 22[0.0%] 26[0.0%] 30[0.0%]
3[0.7%] 7[0.0%] 11[0.0%] 15[0.0%] 19[0.0%] 23[0.0%] 27[0.0%] 31[0.0%]
Mem:\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|180G/252G  Tasks: 65, 178 thr, 406 kthr; 2 running
Swap\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|0K/0K  Load average: 0.11 0.12 0.09
Uptime: 74 days, 07:09:18
```

Main          1270
PID USER         PRI NI VIRT  RES SHR S CPU% MEM% TIME+    COMMAND
2119928 root      20 0 226M 5628 3432 R 1.3 0.0 0:00.16 htop
83078 qemu      20 0 21.6G 16.3G 10620 S 0.7 6.4 4:018:13 /usr/lib/exec/q
83100 qemu      20 0 21.6G 16.3G 10620 S 0.7 6.4 7:49:20 /usr/lib/exec/q
1 root      20 0 247M 15252 8824 S 0.0 0.0 1:26.89 /usr/lib/system
1147 root      20 0 142M 34104 18656 S 0.0 0.0 12:55:10 /usr/lib/system
1192 root      20 0 106M 10496 6592 S 0.0 0.0 0:13.50 /usr/lib/system
1271 root      20 0 6717M 5552 4828 S 0.0 0.0 0:04.33 /usr/bin/rpcbind
1272 root      16 -4 129M 2672 1812 S 0.0 0.0 1:07.97 /sbin/auditd
1273 root      16 -4 129M 2672 1812 S 0.0 0.0 0:00.32 /sbin/auditd
1334 root      20 0 9098M 7404 6072 S 0.0 0.0 0:12.27 /usr/lib/system
1337 root      20 0 9505M 9420 7000 S 0.0 0.0 0:12.81 /usr/lib/system
1347 root      20 0 122M 5612 4768 S 0.0 0.0 24:42.40 /usr/sbin/irqbalance

```
F1 Help F2 Setup F3 Search F4 Filter F5 Tree F6 SortF7Nices F8 Ice F9Kill F10Quit
```

*Figure 6.12: Example aspect of command htop*

# Command mpstat

This command is part of the sysstat package, which requires to be installed to be used. This application reports processors-related statistics. Figure 6.13 shows an example output without any option or argument specified:

```
[root@server ~]# mpstat
Linux 4.18.0-305.30.1.el8_4.x86_64 (server) 13/08/22 x86_64 (32 CPU)

14:00:47 CPU %usr %nice %sys %iowait %irq %soft %steal %guest %gnice %idle
14:00:47 all 0.05 0.00 1.86 0.27 0.19 0.17 0.00 8.16 0.00 89.32
```

*Figure 6.13: Output example for the command mpstat*

The command mpstat allows the options -N to specify the NUMA nodes and the option -P to indicate the processors to display the statistics. The arguments available for the application are interval and count, which will create a count number of reports every interval seconds. Figure 6.14 shows an example to generate five reports each 6 seconds: