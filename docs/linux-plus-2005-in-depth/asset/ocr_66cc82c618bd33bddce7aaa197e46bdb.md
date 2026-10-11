# # TROUBLESHOOTING INSTALLATION

Hardware is detected by the Linux kernel at system startup. However, this information is displayed too quickly to read. In addition, the software programs loaded during system startup are hidden by default during the graphical boot process; you must use your mouse to click Show Details during the graphical boot process to see them. Like the hardware information, program information is also displayed too fast to read. Fortunately, the system logs all information regarding hardware detection and the startup of system processes in log files that can be viewed at a later time.

To view the hardware detected during boot time, you can use the dmesg command shown in the following output. This information is also stored in the /var/log/dmesg log file:

```
[root@server1 root]# dmesg | tail
Bluetooth: RFCOMM socket layer initialized
Bluetooth: RFCOMM TTY layer initialized
parport0: PC-style at 0x378 [PCSPP,TRISTATE,EPP]
parport0: Printer, Brother HL-1440 series
parport_pc: Via 686A parallel port: io:0x0x378
lp0: using parport0 (polling).
lp0: console ready
aggpart: Found an AGP 2.0 compliant device at 0000:00:00.0.
aggpart: Putting AGP V2 device at 0000:00:00.0 into 1x mode
aggpart: Putting AGP V2 device at 0000:01:00.0 into 1x mode
[root@server1 root]#
```

You can also view the system processes that started successfully or unsuccessfully during boot time by viewing the contents of the /var/log/boot.log or /var/log/messages log files. The boot.log file contains only service startup information, whereas messages contains boot information as well as other messages from the system after boot time. A sample boot.log is shown in the following output:

```
[root@server1 root]# tail /var/log/boot.log
Jul 16 08:38:33 server1 privoxy: privoxy startup succeeded
Jul 16 08:38:34 server1 gpm: gpm startup succeeded
Jul 16 08:38:35 server1 11im: 11im startup succeeded
Jul 16 08:38:36 server1 canna: succeeded
Jul 16 08:38:36 server1 crond: crond startup succeeded
Jul 16 08:38:38 server1 xfs: xfs startup succeeded
Jul 16 08:38:38 server1 anacron: anacron startup succeeded
Jul 16 08:38:38 server1 atd: atd startup succeeded
Jul 16 08:38:38 server1 readahead: Starting background readahead:
Jul 16 08:38:39 server1 rc: Starting readahead: succeeded
[root@server1 root]#
```