# Review Questions

+   1. A backup plan does not normally include the following:
+      a. a list of tape drive prices
+      b. times when backups are performed
+      c. the location of critical files on the system
+      d. a recommended time to replace old tape cartridges with new ones

RAID-0 — A RAID level that uses striping to improve disk performance without adding any fault tolerance.

RAID-1 — A RAID level that uses disk mirroring to significantly improve fault tolerance. Disk read performance is also improved, but disk write performance suffers.

RAID-3 — A RAID level that uses striping with parity information to improve performance and increase fault tolerance.

RAID-5 — A RAID level in which striping with parity is spread across all disks in the RAID array (compared to RAID-3, in which the parity information is stored on a single hard disk).

RAID-Linear — A storage technique in which multiple physical devices are combined into a single logical device.

RAID subsystem — A hardware-controlled RAID device containing a CPU and other components to control the array of hard disks.

redundant arrays of inexpensive disks — See RAID.

restore — To copy data from a backup location (for example, a tape cartridge) onto the file system where that data is normally used, and from which it was unintentionally lost.

rotating log files — The process of moving existing log files to another file name and location for archiving or review.

selector — A field in the syslog.conf file that determines what events are being logged. A selector is composed of a facility and a priority.

SIGHUP — A signal sent to a logging daemon to instruct the daemon to reread its configuration files and the log file to which it writes. Sometimes called HUP.

striping — A data storage technique in which parts of a file are written to more than one disk in order to improve performance. See RAID-3 and RAID-5.

syslog.conf — The configuration file used to control how and where messages are logged by syslogd and klogd.

system clock — An internal clock maintained by the Linux kernel whenever the system is turned on. Initialized based on the hardware clock. Maintained accurately on large networks by relying on a network time server using the Network Time Protocol (NTP).

timestamp — The date and time when an event being logged occurred.

write caching — A feature of some storage systems in which information that is to be written to a file system (particularly a RAID file system) is stored in memory temporarily in order to improve the overall read/write performance of the file system.