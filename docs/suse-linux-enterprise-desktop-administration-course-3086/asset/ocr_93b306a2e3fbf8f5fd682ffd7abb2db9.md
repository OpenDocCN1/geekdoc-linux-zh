# Summary

+   - The Linux file system is arranged hierarchically using a series of directories to store files.
+   - Regardless of the number of file systems, there is only one root directory in Linux, denoted by a “/” character.
+   - Linux directories and files follow the File System Hierarchy Standard (FHS) and their location can be described using absolute or relative pathnames. You can view your current directory with the pwd command or change directories using the cd command.
+   - The /bin and /sbin directories contain executable binary programs. There are many other directories throughout the file system that have the name bin and sbin.
+   - The /boot directory contains information used to load the Linux kernel.
+   - The /dev directory contains character and block-oriented device files that are used to identify most hardware devices on the Linux system. Each device file contains a major number that identifies the device driver in the Linux kernel and a minor number that identifies the instance of the particular device. You can use the mknod command to create device files.
+   - Most system configuration information is stored in text files under the /etc directory and shared libraries are stored under the /lib directory.
+   - Home directories are typically located under the /home directory and named for their user account (e.g., /home/gecko). The root user’s home directory is always /root.
+   - The /media and /mnt directories typically contain mount point subdirectories that are used to mount and access removable media such as CD-ROMs, CD-RWs, DVDs, and floppies. The system typically automatically mounts these devices, but you can manually mount and unmount devices to these directories using the mount and umount commands.
+   - Non-Linux partitions are typically mounted to directories that begin with /data or /windows.
+   - The /usr and /opt directories store most system and user applications. In addition, many applications store application data in the /srv directory and temporary files in the /tmp directory.
+   - Log files, spool directories, and application-specific files are typically stored under the /var directory.
+   - The /proc and /sys directories are virtual directories in system memory that contain information that is exposed by the Linux kernel, including process, hardware, network, and version information. As a result, files in these directories are often used in system troubleshooting.
+   - There are many types of files that can exist on the Linux file system, such as normal files (text files, data files, executable programs), directories, device files, linked files, sockets, and named pipes (FIFOs). You can use various options to the ls command to view filename information.
+   - The touch command can create new files or update the time stamp on an existing file.