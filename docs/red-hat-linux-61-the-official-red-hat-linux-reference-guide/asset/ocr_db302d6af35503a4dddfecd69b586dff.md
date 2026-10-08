Chapter 5. The proc File System 61

# 5.3.4. /proc/fs

This directory shows which file systems are exported. If running an NFS server, typing cat /proc/nfs/exports will display the file systems shared and the permissions granted for those file systems. For more sharing file system with NFS, see Chapter 9 Network File System (NFS).

# 5.3.5. /proc/ide/

This directory holds information about IDE devices on the system. Each IDE channel is represented as a separate directory, such as /proc/ide/ide0 and /proc/ide/ide1. In addition, drivers file is also available, providing the version of the number drivers used on the IDE channels:

```
ide-cdrom version 4.59
ide-floppy version 0.97
ide-disk version 1.10
```

Many chipsets also provide an informational file in this directory that gives additional data concerning the drives connected through the channels. For example, a generic PIIX4 Ultra 33 chipset produces a /proc/ide/piix that will tell you whether DMA or UDMA is enabled for the devices on the IDE channels:

| | PIIX4 Ultra 33 Chipset |
|---| Primary Channel | Secondary Channel |
| --- | --- |
| enabled | enabled |
| drive0 | drivel | drive0 | drivel |
| DMA enabled: yes | no | yes | no |
| UDMA enabled: yes | no | no | no |
| UDMA enabled: 2 | X | X | X |
| DMA | | |
| PIO | | |

Navigating into the directory for an IDE channel, such as ide0, provides additional information. The channel file provides the channel number, while the model tells you the bus type for the channel (such as pci).

# 5.3.5.1. The Device Directory

Each IDE channel is a device directory. The name of the device directory corresponds to the drive letter in the /dev/ directory. For instance, the first IDE drive on ide0 would be hda.

> Note
There is a symbolic link to each of these device directories in the /proc/ide/ directory.

Each device directory contains a collection of information and statistics. The contents of these directories vary according to the type of device connected. Some of the most useful files common to many devices include: