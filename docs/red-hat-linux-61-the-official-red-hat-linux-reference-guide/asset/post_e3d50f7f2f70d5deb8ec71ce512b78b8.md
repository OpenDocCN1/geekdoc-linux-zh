
# Chapter 5. The proc File System

| < 2K | 2K | 4K | 8K | 16K | 32K | 64K | 128K+ |
|---|---|---|---|---|---|---|---|---|
| Reads | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Writes | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

scsill:0:6:0
Device using Narrow/Sync transfers to 10.0 MByte, offset 15
Transinfo settings: current(25/15/0), goal(12/15/0), user(12/15/0)
Total transfers 132 (0 reads and 132 writes)

| < 2K | 2K | 4K | 8K | 16K | 32K | 64K | 128K+ |
|---|---|---|---|---|---|---|---|---|
| Reads | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Writes | 0 | 0 | 0 | 1 | 131 | 0 | 0 | 0 |

This output reveals the transfer speed to various SCSI devices connected to the controller on channel ID, as well as detailed statistics concerning the amount and sizes of files read or written by device. For example, this controller is communicating with the CD-ROM at 20 megabytes per second, while the tape drive is only communicating at 10 megabytes per second.

## 5.3.9. /proc/sys/

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

```bash
echo 1 > /proc/sys/sysrq
```

This will change the System Request Key from 0 (off) to 1 (on).

The purpose of the System Request Key is to allow immediate input to the kernel through simple key combinations. For example, the System Request Key can be used to immediately shut down or restart a system, sync all mounted file systems, or dump information to your console. This feature is most useful when developing a kernel or when experiencing system freezes. However, it is

Various variables in /proc/sys/dev/cdrom, as autoclose and checkmedia, can be used to control the system's CD-ROM. Use the echo command to enable or disable these features.

## Chapter 5. The proc System

If RAID support is compiled into the kernel, a /proc/sys/dev/raid/ directory will be available with at least two files in: speed_limit_min and speed_limit_max. These settings determine the acceleration of RAID devices for I/O intensive tasks, such as resyncing the disks.

### 5.3.9.2. /proc/sys/fs/

This directory contains an array of options and information concerning various aspects of the file system, including quota, file handle, inode, and entry information. The binfmt_misc directory is used to provide kernel support for miscellaneous binary formats. The important files in /proc/sys/fs/ include:

- dentry-state — Provides the status of the directory cache. The file looks similar to:
57411 52939 45 0 0 0
The first number reveals the total number of directory cache entries, the second number displays the number of unused entries. The third number shows the number of seconds between a directory has been freed and when it can be reclaimed, and the fourth the pages requested by the system. The last two are not used and display only zeros.
- dquot-nr — Shows the number of cached dquot entries.
- file-max — Change the maximum number of file handles that the kernel will allocate. Raising the value in this file can resolve errors caused by a lack of available file handles.
- file-nr — Displays the number of allocated file handles, used file handles, and the maximum number of file handles.
- overflowuid — Defines the fixed group ID and user ID, respectively, for use with file systems that only support 16-bit group user IDs.
- super-max — Controls the maximum number of superblocks available.
- super-nr — Displays the current number of superblocks in use.

### 5.3.9.3. /proc/sys/kernel/

This directory contains a variety of configuration files that directly affect the operation of the kernel. Some of the most important files include:

- acct — Controls the suspension of process accounting based on the percentage of free space available on the file system containing the log. By default, the file looks like this:
2 30
The second value sets the threshold percentage of free space when logging will be suspended, while the first value dictates the percentage of free space for logging to resume. The third value sets the interval, at the kernel polls the file system to see if logging should be suspended or resumed.
- cap-bound — Controls the capability bounding settings, which provides a list of capabilities for any process on the system. If a capability is not listed here, then no process, may gain it. The idea is to make the system more secure by ensuring that certain things cannot happen, at beyond a certain point in the boot process.

For a valid list of values for this virtual file, consult /usr/src/linux-2.4/include/linux/capability.h. More information on capability bounding is available at the following URL: http://lwn.net/1999/1202/kernel.php3.

- ctrl-alt-del — Controls [Ctrl]-[Alt]-[Delete] will gracefully restart the computer using (value 0) or force an immediate reboot without syncing the dirty bits to disk (value 1).
- domainname — Configures the system domain name, such as example.com.
- hostname — Configures the system hostname, as www.example.com.
- hotplug — Configures the utility used when a configuration change is detected by the system. This is primarily used with USB and Card PCI. The default value of /sbin/hotplug should not be changed unless you are testing a new program to fulfill this role.
- modprobe — Sets the location of the proc directory to load modules. The default value of /sbin/modprobe signifies that kmod will actually load the module when necessary.
- msgmax — Sets the maximum size of any message sent from one process to another. The default is 8192 bytes. You should be careful about raising this value, as queued messages are stored in non-swappable kernel memory.
- msgnnb — Sets the maximum number of message queue identifiers. The default is 16384.
- osrelease — Lists the kernel release number. This file can only be altered by changing the kernel source and recompiling.
- ostype — Displays the type of operating system. By default, this is set to Linux, and its value can only be changed by changing the kernel source and recompiling.
- overflow — Defines the fixed group ID and user ID, respectively, for you that only support group and user IDs.
- panic — Defines the number of seconds the kernel will postpone rebooting when the system experiences a kernel panic. By default, the value is set to 0, which disables automatic rebooting after a panic.
- printk — This file controls a variety of settings for printing or logging error messages. Each error message reported by the kernel has a loglevel associated with it that defines the importance of the message. The loglevel values break down in this order:
  - 0 Kernel emergency. The system is unusable.
  - 1 Kernel alert. Action must be taken immediately.
  - 2 Condition of the kernel is considered critical.
  - 3 General kernel error condition.
  - 4 General kernel warning condition.
  - 5 Kernel notice of a normal but significant condition.
  - 6 Kernel informational message.
  - 7 Kernel debug-level.

Four values are found in the printk file:
6 4 7
Each of these values defines a different rule for dealing with messages, called the console loglevel, defines the lowest priority of messages that will be printed to the console. (Note that, the lower the priority, the higher the loglevel number). The second value sets the default loglevel for messages without an explicit loglevel attached to them. The third value sets the lowest possible loglevel configuration for the console loglevel. The last value sets the default value for the console loglevel.
