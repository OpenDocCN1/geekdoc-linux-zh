# FILE SYSTEMS AND DATA MEDIA 111

+   - File systems can be mounted either with read/write access (rw) or with read-only access (ro).

+   - The root partition cannot be unmounted; thus at start-up, it is initially mounted readonly, and only after the file system check is carried out is the access mode changed to write access by means of the remount option. At system shutdown, the remount option is used again to change the mode back to readonly operation.

+   - Partitions can be mounted with the sync option, which prevents modifications from being temporarily stored in the buffer cache. The default is async, which allows buffering. For diskettes, it may be sensible to write all data unbuffered before the user removes the floppy disk from the drive.

+   - Nonprivileged users too should be allowed to mount disks or CD-ROMs. This is achieved by entering the user option in the /etc/fstab file. The system uses the options noexec, nosuid, and nodev as the default. The system administrator can overwrite these options in the /etc/fstab file.

+   - The defaults option implies the options rw, suid, dev, exec, auto, nouser, and async, as discussed above.

Individual file systems may have additional options. Thus, the FAT file system nor HPFS has user IDs. Therefore, a user and group ID can be globally assigned to the whole file system when it being mounted. This is done by means of the uid= and gid= options, each followed by the numeric identification. Assignment of permissions too can only be carried out for the entire file system, by specifying the corresponding umask= during mounting. Further options are extensively described in the man for mount (8).

# 4.5.3 The automounter amd or autofofs

The easiest solution for the user is the automounter (amd or autofofs) which, every time a user changes directory, temporarily mounts the corresponding file system. If the file system is not used for a certain time, it is automatically unmounted. It is, however, also possible to trigger the unmounting in such a way that a user can remove a data medium from the drive immediately after usage, without having to wait for the timeout. The full power of the automounter, however, is only unleashed in network operation; more detailed information on this subject is given in Section 18.3. The latest kernel version integrates autofofs which is soon supposed to replace the automounter.