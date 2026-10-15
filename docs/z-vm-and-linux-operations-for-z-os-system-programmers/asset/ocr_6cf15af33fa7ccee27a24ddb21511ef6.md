> Note: A good practice is to change the system DASDs labels after you have copied your z/VM system. Refer to 4.3.3, "Relabeling the system volumes" on page 165 for more details.

This copy operation results in a brand new z/VM system, ready to IPL. The IPL must be FORCEd, because no warm-start data was recorded. For more information about warm-start data, refer to 5.2.1, "z/VM IPL workflow" on page 230.

> Important: Although spool files such as the reader, printer or punch files can be lost during the copy process, this should not cause a problem restarting z/VM and the Linux virtual machines that were running in the environment.
> 
> This method cannot be applied to backups of running Linux machines. Back up of running Linux machines can lead to data inconsistency.

# 8.4.3 Linux backup tools

Linux distributions include tools for backing up and restoring data. Several are basic tools, such as tar or cpio; others are more complex, such as IBM Tivoli Storage Manager.

Although this section introduces several tools provided by the Linux distributions to perform backups, it is by no means a complete list.

> Important: All the tools described in this section do not perform consistency checks or data integrity control.

# Tar archiving utility

The tar utility is a standard UNIX tool to create an archive from a set of files or directories. This archive can then be compressed and saved to another set of disk or a tape. See Example 8-24.

Example 8-24 Archiving files using tar

```
lnxquill:"# tar cvf varlog_backup.tar /var/log
tar: Removing leading '/' from member names
/var/log/
/var/log/yaST2/
/var/log/yaST2/y2logRPM
/var/log/yaST2/y2log
/var/log/yaST2/y2logmkinitrd
/var/log/yaST2/y2log_bootloader
```