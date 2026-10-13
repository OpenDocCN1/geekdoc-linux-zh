```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/sda5: block grace period: 0 days, file grace period:
0 days
```

You can specify the grace period in days, hours, minutes, or even seconds. For example, in the following, the grace period for the disk space limit (in blocks) is 7 days, and the grace period for the number of files (inodes) is only 5 hours:

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/sda5: block grace period: 7 days, file grace period:
5 hours
```

# fdformat

Syntax:

```
fdformat floppy-device
```

The fdformat program does a low-level format on a floppy device. For example,

```
fdformat /dev/fd0H1440
```

formats the first floppy disk (/dev/fd0) using the high-density 1.44MB format.

# fdisk

The fdisk program works with one disk at a time, and even though it provides a simple, inelegant user interface, it actually provides quite a bit more flexibility than the Disk Druid tool.

fdisk has a simple, command-prompt-oriented interface. It is also the default partitioning tool available after you have already installed Red Hat Linux. You can run fdisk from the command line by using the following syntax:

```
fdisk hard disk device
```