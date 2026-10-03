# 5. Allocating Windows Disk Partitions to RHEL 9

In the previous chapter, we looked at installing Red Hat Enterprise Linux 9 on the same disk as Windows. This so-called “dual boot” configuration allows the user to have both operating systems installed on a single disk drive with the option to boot one or the other when the system is powered on.

This chapter is intended for users who have decided they like RHEL 9 enough to delete Windows entirely from the disk and use the resulting space for Linux. In the following sections, we will work through this process step by step.

# 5.1 Unmounting the Windows Partition

If the steps in the “Dual Booting RHEL 9 with Windows” chapter were followed to mount the Windows partition from within RHEL 9, steps should be taken to unmount the partition before continuing with this chapter. Assuming that the Windows partition was mounted as /mnt/windows, it can be unmounted as follows:

```
# umount /mnt/windows
```

The /etc/fstab file should also be edited to remove the /mnt/windows auto-mount if it was previously added.

# 5.2 Deleting the Windows Partitions from the Disk

The first step in freeing up the Windows partition for use by RHEL is to delete that partition. Before doing so, however, any data you need to keep must be backed up from both the Windows and RHEL partitions. Having done that, it is safe to proceed with this chapter.

To remove the Windows partitions, we first need to identify the disk on which they reside using the fdisk tool:

```
# fdisk -l
Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors
Disk model: VMware Virtual NVMe Disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimum): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 7A38CD86-091E-4781-BFB0-928FD383C935

Device     Start       End Sectors  Size Type
/dev/nvme0n1p1  2048  206847  204800 100M EFI System
```