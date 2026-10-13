# TABLE 6-4 Basic Filesystem Hierarchy Standard Directories

| Directory | Description |
|---|---|
| / | The root directory, the top-level directory in the FHS. All other directories are subdirectories of root, which is always mounted on some volume. |
| /bin | Essential command line utilities. Should not be mounted separately; otherwise, it could be difficult to get to these utilities when using a rescue disk. |
| /boot | Includes Linux startup files, including the Linux kernel. The default, 500MB, is usually sufficient for a typical modular kernel and additional kernels that you might install during the RHCE or RHCSA exam. |
| /dev | Hardware and software device drivers for everything from floppy drives to terminals. Do not mount this directory on a separate volume. |
| /etc | Most basic configuration files. Do not mount this directory on a separate volume. |
| /home | Home directories for almost every user. |
| /lib | Program libraries for the kernel and various command line utilities. Do not mount this directory on a separate volume. |
| /media | The mount point for removable media, including floppy drives, DVDs, and Zip disks. |
| /misc | The standard mount point for local directories mounted via the automounter. |
| /mnt | A legacy mount point; formerly used for removable media. |
| /net | The standard mount point for network directories mounted via the automounter. |
| /opt | Common location for third-party application files. |
| /proc | Currently running kernel-related processes, including device assignments such as IRQ ports, I/O addresses, and DMA channels, as well as kernel configuration settings such as IP forwarding. As a virtual filesystem, Linux automatically configures it as a separate filesystem in RAM. |
| /root | The home directory of the root user. Do not mount this directory on a separate volume. |
| /sbin | System administration commands. Don't mount this directory separately. |
| /selinux | Currently configured settings associated with Security Enhanced Linux. Do not mount this directory on a separate volume. |
| /smb | The standard mount point for remote shared Microsoft network directories mounted via the automounter. |
| /srv | Commonly used by various network servers on non-Red Hat distributions. |
| /tftpboot | Included if the TFTP server is installed. |
| /tmp | Temporary files. By default, Red Hat Enterprise Linux deletes all files in this directory periodically. |
| /usr | Small programs accessible to all users. Includes many system administration commands and utilities. |
| /var | Variable data, including log files and printer spools. |