+   * CPU/gikern
+   * CPU/giwait
+   * CPU/gidle
+   * Proc/runque
+   * Proc/swpque
+   * Proc/pswitch
+   * Mem/Real/$free
+   * Mem/Real/$comp
+   * Mem/Virt/pagein
+   * Mem/Virt/pageout
+   * Mem/Virt/pgpggin
+   * Mem/Virt/pgpgout
+   * PagSp/totalseed
+   * LAN/ent0/framesout
+   * LAN/ent0/framesin
+   * LAN/ent0/xmitdrops
+   * LAN/ent0/recvdrops
+   * LAN/ent0/xmitque
+   * Disk/hdisk0/busy
+   * Disk/hdisk1/busy
+   * Disk/hdisk2/busy
+   * Disk/hdisk3/busy
+   * Disk/hdisk4/busy
+   * Disk/hdisk5/busy

The retain line of this example is configured to keep eight days' worth of performance data, one day per file. The next line, frequency, is set to capture data once every 600,000 milliseconds, or once every 10 minutes. The start line is used to instruct xmservd when to collect data, in this example Sunday (day 0) through Saturday (day 6), from Midnight until 23:50. All of the remaining lines in the file are which performance metrics to collect. These metrics are collected in files named aizo, which are located in /etc/perf. With this example of the retain line, we could expect to see files in /etc/perf named aiz.o.1 (today) through aiz.o.8 (one week ago).

During installation of the agent, the xmservd daemon is configured as an inetd daemon, with the proper line added to /etc/inetd.conf. In order to have xmservd start automatically at system boot time, the following lines should be added to the end of /etc/rc.tcpip:

```
/usr/bin/sleep 10
/usr/bin/xmpexe
```

The sleep command is necessary to allow all the other TCP/IP processes to complete initializing, and the xmpexe command is used to initialize the xmservd daemon. After being initialized, the xmservd daemon will respawn itself as configured by the frequency and start lines in the configuration file.