# # Debugging

The hdparm utility elicits various PATA/SATA disk parameters from the underlying kernel driver. To benchmark disk read speeds on a SATA drive, for example, do this:

```
```bash
bash> hdparm -T -t /dev/sda
/dev/sda:
  Timing cached reads:   2564 MB in  2.00 seconds = 1283.57 MB/sec
  Timing buffered disk reads:  132 MB in  3.03 seconds =  43.61 MB/sec
```
```

For the full capabilities of hdparm, read the man pages.

*Self-Monitoring, Analysis, and Reporting Technology* (SMART) is a system built in to many modern ATA and SCSI disks to monitor failures and perform self-tests. A user-space daemon named smartd collects the information gathered by SMART-capable disks with the help of the underlying device driver. Look at the man pages of smartd, smartctl, and smartd.conf to learn how to obtain health status from SMART-enabled disks.

If your distribution doesn't prepackage hdparm and SMART tools, you may download them from http://sourceforge.net/projects/hdparm/ and http://sourceforge.net/projects/smartmontools/, respectively.

Files under /proc/ide/ contain information about IDE disk drives on your system. To obtain the geometry of the first IDE disk, for example, look at the contents of /proc/ide/ide0/hda/geometry. Information pertaining to SCSI devices is available under /proc/scsi/. You can gather disk partition information from /proc/partitions.

The sysfs directory of interest for IDE devices is /sys/bus/ide/ and for SCSI is /sys/bus/scsi/. In addition, each block device active on the system owns a subdirectory under /sys/block/, which contains associated request queue parameters, constituent partition details, and state information.

Some kernel configuration options are available that trigger the emission of debug output from the block subsystem. CONFIG_BLK_DEV_IO_TRACE provides the ability to trace the block layer. CONFIG_SCSI_CONSTANTS and CONFIG_SCSI_LOGGING turn on SCSI error reporting and logging, respectively.

The linux-ide mailing list is the forum to discuss questions related to the Linux-IDE subsystem. Subscribe to the linux-scsi mailing list and browse through its archives for discussions pertaining to the Linux-SCSI subsystem.