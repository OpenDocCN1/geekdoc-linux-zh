drwxr-xr-x   3 root     root         25600 Aug  6 19:05 /dev
 drwxr-xr-x  10 root     root         2048 Aug  6 19:05 /etc
 drwxr-xr-x   4 root     root         1024 Aug  6 15:28 /home
 drwxr-xr-x   3 root     root         2048 Aug  6 03:51 /lib
 drwxr-xr-x   2 root     root        12288 Aug  6 03:36 /lost+found
 drwxr-xr-x   2 root     root         1024 Oct  6  1997 /mnt
 dr-xr-xr-x   5 root     root            0 Aug  6 12:04 /proc
 drwx--x--    3 root     root         1024 Aug  6 11:39 /root
 drwxr-xr-x   2 root     bin          2048 Aug  6 03:53 /sbin
 drwxr-xr-x   2 root     root         1024 Apr 27  1996 /shlib
 drwxrwxrwt   3 root     root         1024 Aug  6 22:20 /tmp
 drwxr-xr-x  23 root     root         1024 Jun  8  1994 /usr
 drwxr-xr-x  16 root     root         1024 Jun  8  1994 /var

In /bin, you have the main binaries for the operating system. These include but are not limited to cd, ls, rm, cat, ftp, login, mail, ln, kill, pwd, and the user shells (bash, csh, zsh, and so on). The /sbin directory are system administrator's binaries. These include cardmgr, fdisk, halt, kernel, liio, mkfs, and sologin.

In /boot, you have the various files for LOADLlO or LILO that enable booting.

Your devices, including your mouse and terminals, are kept in /dev. This is the device directory. It also includes modems, printers, hard drives, and anything that you connect to the computer.

The /etc directory is the miscellaneous directory for all the files the system needs but isn't exactly sure where they need to go. That's how the /etc directory probably started out— but now it's expected to contain certain files such as /etc/hosts and /etc/services.

There are important subdirectories in /etc. They include pcmcia, ppp, rc.d (which contains the startup and shutdown scripts), slip, and skel (which contains the files that are copied into users' home directories as they are created).

User's home directories are defaulted to /home. However, you can set up your own directories for storing user accounts if you want. The root account's home directory is /root.

The system libraries are stored in /lib. These are 32-bit ELF shared objects or ELF 32-bit executables. There is also the /lib/modules directory, which stores the object files for the kernel modules. The /shlib directory is for SCO-compatible files.

The /lost+found directory is where the system sends inodes that have data but don't have a directory to belong to. This may be caused by a disk crash or if the system is abruptly shut down.

The /mnt and /tmp directories are temporary directories. The /mnt directory is a temporary mount point directory. The /tmp directory is a temporary file storage, especially if disk quota is enabled and a user temporarily needs the disk space. The /proc directory is used for enabling file system processes. These include disk I/O processes, memory, and CPU access.

The /usr directory contains mostly local programs and files. The /usr directory contains links to other directories or subdirectories. The /usr/X11 and /usr/X11R6