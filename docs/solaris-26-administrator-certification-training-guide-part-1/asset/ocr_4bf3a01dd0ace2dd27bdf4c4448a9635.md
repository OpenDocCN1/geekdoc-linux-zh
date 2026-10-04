To check a file system manually, follow these steps:

+   1. Become superuser.
2. Unmount the file system.
3. Type `fsck` and press Enter.

All file systems in the /etc/vfstab file with entries greater than zero in the fsck pass field are checked. You can also specify the mount point directory or /dev/rdsk/ c0t0d0s... as arguments to fsck. The fsck command requires the raw device filename.

Any inconsistency messages are displayed. The only way to successfully change the file system and correct the problem is to answer "yes" to these messages.

**NOTE.** The `fsck` command has an option `-y` that will automatically answer yes to every question. But be careful: if `fsck` asks to delete a file, it will answer yes and you will have no control over it. If it doesn't delete the file, however, the file system remains unclean and cannot be mounted.

+   4. If you corrected any errors, type `fsck` and press Enter. `fsck` might not be able to fix all errors in one execution. If you see the message FILE SYSTEM STATE NOT SET TO OKAY, run the command again and continue to run `fsck` until it runs clean with no errors.
5. Rename and move any files put in lost+found. Individual files put in the lost+found directory by `fsck` are renamed with their inode numbers, and figuring out what they were named originally can be difficult. If possible, rename the files and move them where they belong. You might be able to use the `grep` command to match phrases with individual files and the `file` command to identify file types, ownership, and so on. When whole directories are dumped into lost+found, it is easier to figure out where they belong and move them back.

# Mounting File Systems

After you create a file system, you need to make it available. You make file systems available by mounting them. Using the mount command, you attach a file system to the system directory tree at the specified mount point and it becomes available to the system. The root file system is mounted at boot time and cannot be unmounted. Any other file system can be mounted or unmounted from the root file system at any time.

The various methods used to mount a file system are described in the next sections.

# Creating an Entry in the /etc/vfstab File to Mount File Systems

The /etc/vfstab (virtual file system table) file contains a list of file systems to be automatically mounted when the system is booted to the multiuser state. The system administrator