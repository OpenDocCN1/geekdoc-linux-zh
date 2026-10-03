NOTE
A common misconception is that the fsck pass field specifies the order in which file systems are to be checked. In SunOS system software, the fsck pass field does not specify the order in which file systems are to be checked. During bootup, a preliminary check is run on each file system to be mounted from a hard disk, using the boot script /sbin/rcS, which checks the / and /usr file systems. The other rc shell scripts then use the fsck command to check each additional file system sequentially. They do not check file systems in parallel. File systems are checked sequentially during booting even if the fsck pass numbers are greater than 1. The values can be any number greater than 1.

+   - **fsck pass.** The pass number used by fsck to decide whether to check a file. When the field contains a dash (-), the file system is not checked. When the field contains a value of 1 or greater, the file system is checked sequentially. File systems are checked sequentially in the order that they appear in the /etc/vfstab file. The value of the pass number has no effect on the sequence of file system checking.
- **mount at boot.** Specifies whether the file system should be automatically mounted when the system is booted. The rc scripts located in the /etc directory specify which file system gets mounted at each run level.
- **mount options.** A list of comma-separated options (with no spaces) used when mounting the file system. Use a dash (-) to show no options.

# Using the Command Line to Mount File Systems

File systems can be mounted from the command line by using the mount command. The commands in Table 6.3 are used from the command line to mount and unmount file systems.

TABLE 6.3
FILE SYSTEM COMMANDS

| Command | Description |
|---|---|
| mount | Mounts specified file systems and remote resources. |
| mountall | Mounts all file systems specified in a file system table (vfstab). |
| umount | Unmounts specified file systems and remote resources. |
| umountall | Unmounts all file systems specified in a file system table. |

NOTE
File systems are automatically unmounted as part of the system shutdown procedure.

CD-ROMs containing file systems should be automatically mounted when the CD-ROM is inserted if Volume Manager is running. Disks containing file systems that have not yet been automatically mounted can be manually mounted by running the volcheck command.