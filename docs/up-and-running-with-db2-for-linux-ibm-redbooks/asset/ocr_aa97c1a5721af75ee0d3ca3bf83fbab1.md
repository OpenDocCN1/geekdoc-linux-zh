```
11:09:13 AM      190.00
11:09:15 AM     1013.50
11:09:17 AM     1349.00
11:09:19 AM     2071.00
11:09:21 AM     2132.00
11:09:23 AM     1643.50
11:09:25 AM     2194.00
Average:        1399.83
```

```
[root@UDBLNX06 root]# sar -n DEV -s 11:09:25 -f sartest.bin|egrep "eth0|IFACE"
11:09:25 AM     IFACE       rxpck/s   txpck/s    rxbyt/s    txbyt/s
11:09:27 AM     eth0     1187.00   2459.00   1511133.00   3007010.50
11:09:29 AM     eth0     1218.00   2528.50   1558313.00   3078301.00
11:09:31 AM     eth0     1219.00   2534.00   1558488.00   3085869.00
11:09:33 AM     eth0     1209.00   2504.50   1541410.50   3051547.50
11:09:35 AM     eth0     1181.00   2502.50   1504659.50   3050603.50
Average:        eth0     1202.80   2505.70   1534800.80   3054666.30
```

As mentioned in 6.3.3, "Iostat" on page 250, the sar utility is contained in sysstat package; before using this command, you need to make sure sysstat package is installed in your system.

For details about using the sar command, refer to the man help pages for sar or other Linux documentation.

# 6.3.5 Other system monitoring tools

There are also a multitude of Linux system monitoring tools available for monitoring Linux system resource usage, such as the ps command which is known to almost everybody is used to report processes status, pstree can be used to display a tree of processes, netstat for printing network related information, nfsstat for NFS specific statistics, and so forth. In addition, pgrep and pkill commands are very helpful when you want to look up or signal processes based on name and other attributes of processes. And if you like monitoring tools with graphical user interface, utilities like gnome-system-monitor and ksysguard also can be used. For more information, refer to Linux specific documentation.