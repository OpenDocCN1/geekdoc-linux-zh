# Table 6-1 *(continued)*

| Directory | Description |
|---|---|
| `/etc` | Contains most system configuration files and the initialization scripts (in the `/etc/rc.d` subdirectory). |
| `/home` | Conventional location of the home directories of all users. User naba’s home directory, for example, is `/home/naba`. |
| `/lib` | Contains library files for all programs stored in `/sbin` and `/bin` directories (including the loadable driver modules) needed to start Linux. |
| `/media` | A directory for mounting file systems on removable media, such as CD-ROM drives, floppy disks, and Zip drives. Contains the `/media/floppy` directory for mounting floppy disks and the `/media/cdrom` directory for mounting the CD-ROM drive. If you have a CD recorder, you’ll find a `/media/cdrecorder` directory instead of `/media/cdrom`. |
| `/mnt` | A directory for temporarily mounted file systems. |
| `/opt` | Provides a storage area for large application software packages. For example, GNOME and KDE applications are installed in the `/opt` directory. |
| `/proc` | A special memory-resident directory that contains various information about the processes running in the Linux system. |
| `/root` | The home directory for the root user. |
| `/sbin` | Contains executable files representing commands typically used for system-administration tasks and used by the root user. Commands such as `halt` and `shutdown` reside in the `/sbin` directory. |
| `/srv` | Contains data for services (such as Web and FTP) offered by this system. |
| `/sys` | A special directory that contains information about the devices, as seen by the Linux kernel. |
| `/tmp` | A temporary directory that any user can use as a *scratch* directory, meaning that the contents of this directory are considered unimportant and usually are deleted every time the system boots. |
| `/usr` | Contains the subdirectories for many important programs, such as the X Window System (in the `/usr/X11R6` directory) and the online manual. |
| `/var` | Contains various system files (such as logs), as well as directories for holding other information, such as files for printers and mail messages. |