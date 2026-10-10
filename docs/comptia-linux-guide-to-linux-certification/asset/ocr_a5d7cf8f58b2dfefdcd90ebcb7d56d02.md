| Partition | PATA Device Name (Assuming /dev/hda) | SATA/SCSI Device Name (Assuming /dev/sda) |
|---|---|---|
| 1st primary partition | /dev/hda1 | /dev/sda1 |
| 2nd primary partition | /dev/hda2 | /dev/sda2 |
| 3rd primary partition | /dev/hda3 | /dev/sda3 |
| 4th primary partition | /dev/hda4 | /dev/sda4 |
| 1st logical drive in the extended partition | /dev/hda5 | /dev/sda5 |
| 2nd logical drive in the extended partition | /dev/hda6 | /dev/sda6 |
| 3rd logical drive in the extended partition | /dev/hda7 | /dev/sda7 |
| 4th logical drive in the extended partition | /dev/hda8 | /dev/sda8 |
| 5th logical drive in the extended partition | /dev/hda9 | /dev/sda9 |
| nth logical drive in the extended partition | /dev/hdan | /dev/sdan |

Table 5-5 Common hard disk partition device files for /dev/hda and /dev/sda

known as type 82) if that partition is intended for use as virtual memory. This explicit choice of partition type allows for partitions that better suit the needs of a filesystem.

A typical Linux hard disk structure for the primary master PATA hard disk (/dev/hda) can contain a partition for the / filesystem (/dev/hda1) and an extended partition (/dev/hda2) that further contains a swap partition (/dev/hda5) and some free space, as shown in Figure 5-5.

A more complicated Linux hard disk structure for the first SATA/SCSI hard disk might involve preserving the Windows operating system partition, allowing a user to boot into and use the Linux operating system or boot into and use the Windows operating system. This is known as dual booting and is discussed in Chapter 6.

![](bbox=[0.16, 0.68, 0.84, 0.96])