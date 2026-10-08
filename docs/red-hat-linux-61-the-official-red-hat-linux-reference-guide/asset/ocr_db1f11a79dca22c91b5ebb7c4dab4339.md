# Chapter 5. The proc File System

| < 2K | 2K | 4K | 8K | 16K | 32K | 64K | 128K+ |
|---|---|---|---|---|---|---|---||
| Reads | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Writes | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

scsill:0:6:0
Device using Narrow/Sync transfers to 10.0 MByte, offset 15
Transinfo settings: current(25/15/0), goal(12/15/0), user(12/15/0)
Total transfers 132 (0 reads and 132 writes)

| < 2K | 2K | 4K | 8K | 16K | 32K | 64K | 128K+ |
|---|---|---|---|---|---|---|---||
| Reads | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Writes | 0 | 0 | 0 | 1 | 131 | 0 | 0 | 0 |

This output reveals the transfer speed to various SCSI devices connected to the controller on channel ID, as well as detailed statistics concerning the amount and sizes of files read or written by device. For example, this controller is communicating with the CD-ROM at 20 megabytes per second, while the tape drive is only communicating at 10 megabytes per second.

# ## 5.3.9. /proc/sys/

The /proc/sys/ directory differs from others in /proc/ because it does not provide information about the system but also the system administrator to immediately enable and disable kernel features.

> Warning Use when changing settings on a production system using the various files in the /proc/sys/ directory. Changing the wrong setting may render the kernel unstable, requiring a system reboot.

For this reason, be sure the options are valid before attempting to change any value in /proc/sys/.

A good way to determine if a particular file can be configured, or if it is only designed to provide information, is to list it with the -l option at the shell prompt. If the file is writable, it may be used to configure the kernel. A partial listing of /proc/sys/fs looks like this:

```
-r--r--r root 0 May 10 16:14 dentry-state
-rw-r--r-- root 0 May 10 16:14 dir-notify-enable
-r--r--r root 0 May 10 16:14 dquot-nr
-rw-r--r root 0 May 10 16:14 file-max
-r--r--r root 0 May 10 16:14 file-nr
```

In this listing, the dir-notify-enable and file-max can be written to, and therefore, to configure the kernel. The others only provide feedback on current settings.

Changing a value in /proc/sys/ is done by echoing the new value into the file. For example, to enable the System Request on a running kernel, use the command:

```
echo 1 > /proc/sys/sysrq
```

This will change the System Request Key from 0 (off) to 1 (on).

The purpose of the System Request Key is to allow immediate input to the kernel through simple key combinations. For example, the System Request Key can be used to immediately shut down or restart a system, sync all mounted file systems, or dump information to your console. This feature is most useful when developing a kernel or when experiencing system freezes. However, it is