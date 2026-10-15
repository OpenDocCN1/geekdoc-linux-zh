# TIP

The previous command sends the output of ls -alR to a file called listing.txt, and demonstrates part of the power of the Linux command line. At the command line you are able to use files as inputs to commands, or generate files as outputs as shown. For more information about combining commands, see Chapter 30.

We've included a table showing some of the top-level directories that are part of a standard Linux distro in Table 4.1.

# TABLE 4.1 Basic Linux Directories

| Name | Description |
|------|-------------|
| / | The root directory |
| /bin | Essential commands |
| /boot | Boot loader files, Linux kernel |
| /dev | Device files |
| /etc | System configuration files |
| /home | User home directories |
| /initrd | Initial RAM disk boot support (used during boot time) |
| /lib | Shared libraries, kernel modules |
| /lost+found | Directory for recovered files (if found after a file system check) |
| /media | Mount point for removable media, such as DVDs and floppy disks |
| /mnt | Usual mount point for local, remote file systems |
| /opt | Add-on software packages |
| /proc | Kernel information, process control |
| /root | Super-user (root) home |
| /sbin | System commands (mostly root only) |
| /srv | Holds information relating to services that run on your system |
| /sys | Real-time information on devices used by the kernel |
| /tmp | Temporary files |
| /usr | Secondary software file hierarchy |
| /var | Variable data (such as logs); spooled files |

Knowing these directories can aid you in partitioning in any future systems, letting you choose to put certain directories on their own distinct partition.

Some of the important directories in Table 4.1, such as those containing user and root commands or system configuration files, are discussed in the following sections. You use and edit files under these directories when you use Ubuntu.