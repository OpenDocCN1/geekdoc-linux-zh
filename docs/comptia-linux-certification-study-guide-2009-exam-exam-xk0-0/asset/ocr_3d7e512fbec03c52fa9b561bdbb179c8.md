[gabytes]. FAT32, which has a cluster address size of 32-bits, was designed to support a maximum volume size of 2 TB and a maximum file size of 4 GB. The VFAT filesystem introduced before FAT32 was designed to handle long file names. Unlike VFAT, earlier Windows operating systems that used the FAT filesystem allowed files to be named with only eight alphanumeric characters, with a period separating the name from the three-alphanumeric-character extension. This was known as the 8.3 notation. Windows 95, which introduced the VFAT filesystem, supported long filenames that allowed files to have names up to 255 alphanumeric characters.

> **Exam Warning**
> 
> The VFAT filesystem is the preferred filesystem for mounting foreign filesystems.

The NTFS, introduced to support the Microsoft Windows NT operating system, provided several new features unlike the previous filesystems. For example, NTFS provides filesystem security, Unicode, compression, and journaling. The maximum volume size is approximately 256 TB and the maximum file size is 16 EB (Exabytes).

# EXERCISE 3.1: Verifying the Current Filesystem Partition Type id

For this exercise, you will enter the `fdisk` command to obtain a listing of the current filesystems partition types implemented and the filesystem partition types available. This exercise displays the specific primary disk drive attached to your system, the corresponding disk geometry, and the associated filesystem.

Complete the following:

+   1. From the root command prompt, enter the following: `fdisk /dev/sda`.
+   2. Press the **Enter** (Return) key.
+   3. From the `fdisk` prompt, enter the `p` option to print the device partition table.
+   4. Review the system id (for example, 83) for each partition.
+   5. From the `fdisk` prompt, enter the `l` option to list the known various partition types.
+   6. Cross-reference your partition type to the list presented.
+   7. From the `fdisk` prompt, enter the `q` option to quit.