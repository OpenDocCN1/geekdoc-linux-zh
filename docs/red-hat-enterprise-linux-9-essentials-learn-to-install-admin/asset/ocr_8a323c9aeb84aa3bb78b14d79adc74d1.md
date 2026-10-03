Once the requisite packages are installed, the next step is to create a directory to use as the mount point for our Windows partition. In this example, we will create a directory named /mnt/windows:

```
# mkdir /mnt/windows
```

To identify the device name that has been assigned to the Windows partition, use the fdisk command as follows:

```
# fdisk -l
```

```
Device Start End Sectors Size Type
/dev/nvme0n1p1 2048 206847 204800 100M EFI System
/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved
/dev/nvme0n1p3 239616 49362943 49123328 23.4G Microsoft basic data
/dev/nvme0n1p4 132933632 134213631 1280000 625M Windows recovery environment
/dev/nvme0n1p5 49362944 51460095 2097152 1G Linux filesystem
/dev/nvme0n1p6 51460096 132933631 81473536 38.8G Linux LVM
```

In the above output, the main Windows partition containing the files we need access to is represented by /dev/nvme0n1p3. Next, we need to run the mount command (assuming the Windows partition is /dev/nvme0n1p3) as follows:

```
# mount /dev/nvme0n1p3 /mnt/windows
```

Check that the mount was successful by listing the contents of the top-level directory of the mount point:

```
# ls /mnt/windows
'$Recycle.Bin' ProgramData swapfile.sys
'Documents and Settings' 'Program Files' 'System Volume Information'
pagefile.sys 'Program Files (x86)' Users
PerfLogs Recovery Windows
```

To automate the mount each time the system is booted, add the appropriate mount line to the /etc/fstab file:

```
/dev/nvme0n1p3 /mnt/windows ntfs defaults 0 0
```

To unmount the Windows file system at any time:

```
# umount /mnt/windows
```

# 4.4 Summary

RHEL 9 can safely co-exist on the same disk drive as a Windows operating system by creating a dual boot environment. This involves shrinking the Windows system's space to make room for RHEL 9 before performing the installation. Once RHEL has been installed, the boot menu configuration must be modified to include the option to boot from Windows. To access the Windows filesystem from within RHEL, the Fuse NTFS driver needs to be installed and used to mount the Windows partitions.