# 184 *Understanding the Linux File System*

# **Table 3-1 (continued)**

| Directory | Description |
| :--- | :--- |
| /mnt | A directory for temporarily mounted file systems |
| /opt | Provides a storage area for large application software packages. For example, some distributions install the OpenOffice.org office suite in the /opt directory. |
| /proc | A special directory that contains various information about the processes running in the Linux system |
| /root | The home directory for the root user |
| /sbin | Contains executable files representing commands typically used for system-administration tasks and used by the root user. Commands such as *halt* and *shutdown* reside in the /sbin directory. |
| /srv | Contains data for services (such as Web and FTP) offered by this system |
| /sys | A special directory that contains information about the devices, as seen by the Linux kernel |
| /tmp | A temporary directory that any user can use as a *scratch* directory, meaning that the contents of this directory are considered unimportant and usually are deleted every time the system boots |
| /usr | Contains the subdirectories for many important programs, such as the X Window System (in the */usr/X11R6* directory) and the online manual. (Table 3-2 shows *some of the standard* subdirectories in */usr*.) |
| /var | Contains various system files (such as logs), as well as directories for holding other information, such as files for the Web server and anonymous FTP server |

The */usr* and */var* directories also contain a number of standard subdirectories. Table 3-2 lists the important subdirectories in */usr*. Table 3-3 shows a similar breakdown for the */var* directory.

# **Table 3-2** Important */usr* Subdirectories

| Subdirectory | Description |
| :--- | :--- |
| /usr/X11R6 | Contains the X Window System software |
| /usr/bin | Contains executable files for many more Linux commands, including utility programs that are commonly available in Linux but aren't part of the core Linux operating system |
| /usr/games | Contains some old Linux games |
| /usr/include | Contains the header files (file names ending in .h) for the C and C++ programming languages; also includes the X11 header files in the */usr/include/X11* directory and the Linux kernel header files in the */usr/include/linux* directory |