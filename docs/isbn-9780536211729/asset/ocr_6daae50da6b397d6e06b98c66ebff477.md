**lpd** entries show errors encountered by the Line Printer Daemon; these show incorrect configuration or possible exploits.

**dhcpd** entries are from the Dynamic Host Configuration Program Daemon that allows a central server to specify the INET (IP) address that your system should use. These “leases” expire periodically and must be renewed. There may be exploits here.

**last message repeated** entries are used when a message occurs a number of times in succession, to indicate how many times it has been repeated to avoid many lines of log file entries for a repeated event, such as being out of memory or encountering bad disk sectors.

# 13.4.3  syslog

Unlike the messages log file, syslog only logs “problems” and so should be looked at more carefully. Typical problems would be login noting bad passwords when logging in (that also could indicate invalid account names), failed attempts to su, sendmail problems, syslogd conditions (which could indicate cracker activity), and in.telnecd refusing access.

# 13.4.4  kernlog

Not all Linux distributions ship an /etc/syslog.conf file configured to log kernel messages. You certainly want to ensure that yours has a line similar to

```
kern.* /var/log/kernlog
```

This will log kernel messages of all priority to the /var/log/kernlog file. This file will log things such as doing floppy I/O after a floppy change, device drivers being loaded while the system is loaded, system reboots, and attempts to write to a floppy set Read/Only. Although these all could be normal operations, they also could be the work of crackers if no authorized person did them.

Some of these messages are self-explanatory and are listed here. (All of these lines start with the date; some lines are wrapped to fit on the page.)

```
Dec 9 15:10:34 cavu kernel: floppy0: Drive is write protected
Dec 9 15:10:34 cavu kernel: end_request: I/O error, dev 02:00, sector 0
Dec 15 11:16:15 cavu kernel: loading device 'eth0'...
Dec 15 11:16:15 cavu kernel: eth0: Bog us2000, port 0x360, irq 7,
     Auto port, hw_addr 28:44:29:31:0A:69
Dec 15 11:16:31 cavu kernel: eth0: autodetected 10baseT
Dec 17 20:27:25 cavu kernel: VFS: Disk change detected on device 02:00
```