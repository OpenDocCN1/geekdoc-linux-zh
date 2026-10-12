The contents of /proc/sound show the driver version, and also that sound support is loaded as a module and the various devices supported by the loaded driver. This is the same information that is available by examining /dev/sndstat.

# Device Naming Scheme

The naming schemes for the various devices supported by the Linux kernel are documented in the devices.txt file included with the kernel source code. This file contains the names of the devices as well as their major and minor number assignments. Device driver authors should always consult this file before assigning their own device major and minor numbers to avoid conflicts with other devices, as well as follow the instructions contained therein to request the assignment of a permanent set of numbers.

# Assigned Major and Minor Numbers

A complete list of the assigned major and minor device numbers is included with the Linux kernel source code in both ASCII text format and as LaTeX source. The files are /usr/src/linux/Documentation/devices.txt, which is the ASCII version, and /usr/src/linux/Documentation/devices.tex, which is the LaTeX source and the definitive list. This document is not included here in its entirety, but Table 4.1 shows the names, major numbers, and device types for some of the most common devices.

TABLE 4.1 Assigned Device Numbers and Names

| Device Type | Major | Type | Device Name |
|---|---|---|---|
| First IDE controller devices | 3 | block | /dev/hd[a-b]* (1) |
| Second IDE controller devices | 22 | block | /dev/hd[c-d]* (1) |
| Third IDE controller devices | 33 | block | /dev/hd[e-f]* (1) |
| Fourth IDE controller devices | 34 | block | /dev/hd[g-h]* (1) |
| IDE tape devices | 37 | char | /dev/ht0 and /dev/nht0 (2) |
| SCSI disks | 8 | block | /dev/sd[a-p]* (3) |
| SCSI disks | 65 | block | /dev/sd[q-v]* (3) |
| SCSI disks | 66 | block | /dev/sda[g-v]* (3) |
| SCSI disks | 67 | block | /dev/sda[w-z]* and /dev/sdb[a-l]* (3) |
| SCSI CDROM drives | 11 | block | /dev/scd[0-7]* (4) |
| SCSI tape devices | 9 | char | /dev/st[0-9]* and /dev/nst[0-9]* (2) |
| Floppy controller tape devices | 27 | char | /dev/qft* & /dev/n*qft* (2) |
| Parallel port IDE disk devices | 45 | block | /dev/pd* (5) |
| Parallel port ATAPI CDROM devices | 96 | block | /dev/pcd* |