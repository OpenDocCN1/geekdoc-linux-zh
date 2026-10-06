318 Chapter 13 · Understanding the Red Hat Linux File System Layout

# /lost+found: Recovered Files

When you recover a file system, files and file data may be partially recovered. For example, the recovery utility may recover a file's data but not the file's name. Such files are placed by the utility in the /lost+found subdirectory of the root directory of the file system.

# /mnt: Mount Point for Temporarily Mounted File Systems

The /mnt directory exists as the standard parent directory of a set of directories for temporarily mounting file systems. Standard subdirectories include cdrom, a mount point for CD-ROM file systems, and floppy, a mount point for file systems residing on floppy disk.

# /proc: System Information Virtual File System

The Linux /proc directory is a pseudo file system provided by the kernel that contains files and directories that let system administrators and programmers access system information. Some information in the /proc directory can be modified to configure system operation.
Some of the most important files and subdirectories in the /proc directory are summarized in Table 13.5. See the page on /proc for further information on the contents of the /proc directory.

TABLE 13.5 Important Files and Subdirectories of /proc

| File or Subdirectory | Contnets |
| --- | --- |
| [number] | A directory that contains files and subdirectories that describe the process having the same ID as the directory name |
| cpuinfo | Various architecture-dependent information |

Copyright ©2000 SYBEX, Inc., Alameda, CA www.syb.com