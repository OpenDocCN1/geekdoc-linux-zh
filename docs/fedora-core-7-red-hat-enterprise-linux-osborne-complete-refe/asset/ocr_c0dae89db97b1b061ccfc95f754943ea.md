# System Directories

Your Linux directory tree contains certain directories whose files are used for different system functions. For basic system administration, you should be familiar with the system program directories where applications are kept, the system configuration directory (**/etc**) where most configuration files are placed, and the system log directory (**/var/log**) that holds the system logs, recording activity on your system. Both are covered in detail in Chapter 29. Table 30-2 lists the system directories.

# Program Directories

Directories with **bin** in the name are used to hold programs. The **/bin** directory, holds basic user programs, such as login, shells (BASH, TCSH, and zsh), and file commands (**cp**, **mv**, **rm**, **ln**, and so on). The **/sbin** directory holds specialized system programs for such tasks as file system management (**fsck**, **fdisk**, **mkfs**) and system operations like shutdown and startup (**init**). The **/usr/bin** directory holds program files designed for user tasks. The **/usr/sbin** directory holds user-related system operation, such as **useradd** for adding new users.

| Directory | Description |
|---|---|
| /bin | System-related programs |
| /sbin | System programs for specialized tasks |
| /lib | System libraries |
| /etc | Configuration files for system and network services and applications |
| /home | The location of user home directories and server data directories, such as Web and FTP site files |
| /media | The location where removable media file systems like CD-ROMs and floppy disks are mounted |
| /var | The location of system directories whose files continually change, such as logs, printer spool files, and lock files |
| /usr | User-related programs and files. Includes several key subdirectories, such as /usr/bin, /usr/X11, and /usr/share/doc |
| /usr/bin | Programs for users |
| /dev | Device files |
| /sys | The sysfs file system with device information for kernel-supported devices on your system |
| /usr/X11 | X Window System configuration files |
| /usr/share | Shared files |
| /usr/share/doc | Documentation for applications |
| /usr/share/hal | Configuration for HAL removable devices |
| /etc/udev | Configuration for device files |
| /tmp | Directory for system temporary files |