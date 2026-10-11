# Key Concept

There can be a total of no more than four partitions on each disk. These can be all primary or you can have up to three primary and one extended partition.

One more issue must be addressed before you finalize your partition plan. As mentioned in Chapter 2, “Booting Linux,” when LILO is used to boot Linux, it does not recognize beyond the 1023rd cylinder of your hard drive. Therefore, if you are using LILO to boot your system, the partition where LIL0 resides must exist entirely within the first 504MB.

# Interpreting Partition Names

Partitions are named according to the type of disk controller the hard disk contains, the partition, and which partition it is on that disk. Under DOS, the first partition of the first drive would be disk(0) partition(1). Linux refers to the same partition as hdat if it is IDE and sdal if it’s SCSI.

When interpreting partition names, the first letter identifies the type of controller (SCSI or IDE). The d stands for disk; the third letter numbers the disks (the first disk is a, the second is b, and so on); and the last character is the partition number. Table 3.1 shows some partitions.

Table 3.1 Naming Partitions Under Linux
| Name | Controller | Disk | Partition |
| hda1 | IDE controller | first disk | first partition |
| sda1 | SCSI controller | first disk | first partition |
| hdc3 | IDE controller | third disk | third partition |
| sdb4 | SCSI controller | second disk | fourth partition |

# Key Concept

Partition names are based on the type of controller and partition number. Partitions on SCSI drives are referred to as sdan and partitions on IDE drives are named hdan.

# How Many and What Size?

Linux will run just fine with only two partitions, root (/) and swap (swap). All files, applications, and so on, are installed on the root partition. The swap partition is used as virtual memory.