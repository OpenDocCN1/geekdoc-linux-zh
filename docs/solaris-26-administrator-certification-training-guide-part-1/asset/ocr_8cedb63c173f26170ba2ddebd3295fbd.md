# Logical Device Name: Test Item

Logical device names are used with most of the Solaris file system commands to refer to devices. Logical device files in the /dev directory are symbolically linked to physical device files in the /devices directory. Logical device names are used to access disk devices in the following circumstances:

+   - Adding a new disk to the system
- Moving a disk from one system to another
- Accessing (or mounting) a file system residing on a local disk
- Backing up a local file system
- Repairing a file system

Logical devices are organized in subdirectories under the /dev directory by their device types:

| Path | Description |
|---|---|
| /dev/dsk | Block interface to disk devices |
| /dev/rdsk | Raw or character interface |
| /dev/rmt | Tape devices |
| /dev/term | Serial line devices |
| /dev/cua | Dial-out modems |
| /dev/pts | Pseudo terminals |
| /dev/fbs | Frame buffers |
| /dev/sad | STREAMS administrative driver |

Logical device files have major and minor numbers that indicate device drivers, hardware addresses, and other characteristics. Furthermore, a device filename must follow a specific naming convention. A logical device name for a disk drive has the following format:

```
/dev/[r]dsk/cxtxdxsx
```

where

| Symbol | Meaning |
|---|---|
| cx | Refers to the controller number |
| tx | Refers to the SCSI bus target number |
| dx | Refers to the disk number (always 0 except on storage arrays) |
| sx | Refers to the slice or partition number |