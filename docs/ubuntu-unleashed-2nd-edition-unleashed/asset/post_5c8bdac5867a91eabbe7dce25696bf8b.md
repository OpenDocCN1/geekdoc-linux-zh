
The /proc directory can also be used to dynamically alter the behavior of a running Linux kernel by “echoing” numerical values to specific files under the /proc/sys directory.

### NOTE

The Linux kernel has a number of built-in protections, but good system administration security policies and a secure firewall protecting your gateway, router, or Internet-connected system are the best protection you can use.

Other ways to use the /proc directory include

- Getting CPU information, such as the family, type, and speed from /proc/cpuinfo.
- Viewing important networking information under /proc/net, such as active interfaces information under /proc/net/dev, routing information in /proc/net/route, and network statistics in /proc/net/netstat.
- Retrieving file system information.
- Reporting media mount point information via USB; for example, the Linux kernel will report what device to use to access files (such as /dev/sda) if a USB camera or hard drive is detected on the system. You can use the dmesg command to see this information or find information about these devices under the Device File System directory /proc/devfs (see the Linux Devfs FAQ at http://www.atnf.csiro.au/~rgooch/linux/docs/devfs.html if the source code for the Linux kernel is installed). The file /usr/src/linux-2.6/Documentation/usb/proc_usb_info.txt contains general information about USB and the /proc directory, as well as what to expect in files under this directory. Note that devfs might be supported, but will generally be obsolete in the 2.6 kernel because /proc/udev replaces it as a way of managing hot-plug devices on your system.
- Getting the kernel version in /proc/version, performance information such as uptime in /proc/uptime, or other statistics such as CPU load, swap file usage, and processes in /proc/stat.

## Work with Shared Data in the /usr Directory

The /usr directory (nearly 2GB in size if you do a default install) contains software applications, libraries, and other types of shared data for use by anyone on the system. Many Linux system administrators give /usr its own partition. A number of subdirectories under /usr contain the X Window System (/usr/X11R6), manual pages (/usr/share/man), software package shared files (/usr/share/name_of_package, such as /usr/share/emacs), additional application or software package documentation (/usr/share/doc), and an entire subdirectory tree of locally built and installed software, /usr/local.

### NOTE

Although there is a /usr/X11R6 directory, it actually links through to /usr/bin. The reason for this round robin approach is to maintain compatibility with applications that still expect X to reside under /usr/X11R6. X11R7 does away with a separate directory under /usr hence why this link is in place.

## Temporary File Storage in the /tmp Directory

As its name implies, the /tmp directory is used for temporary file storage; as you use Linux, various programs create files in this directory. The /tmp directory is cleaned of stale files each day by the tmpwatch command. (A stale file is any file not used after 10 days.) Ubuntu is configured by default to use tmpwatch to check /tmp each day by settings in your system's scheduling table, /etc/crontab.

## Access Variable Data Files in the /var Directory

The /var directory contains subdirectories used by various system services for spooling and logging. Many of these variable data files, such as print spooler queues, are temporary, whereas others, such as system and kernel logs, are renamed and rotated in use. Incoming electronic mail is usually directed to files under /var/spool/mail.

Linux also uses /var for other important system services. These include the top-most File Transfer Protocol (FTP) directory under /var/ftp (see Chapter 23, “Remote File Serving with FTP”), and the Apache web server’s initial home page directory for the system, /var/www/html. (See Chapter 20, “Apache Web Server Management,” for more information on using Apache.)

## Logging In to and Working with Linux

You can access and use a Linux system in a number of ways. One way is at the console with a monitor, keyboard, and mouse attached to the PC. Another way is via a serial console, either by dial-up via a modem or a PC running a terminal emulator and connected to the Linux PC via a null modem cable. You can also connect to your system through a wired or wireless network using the telnet or ssh commands. The information in this section shows you how to access and use the Linux system using physical and remote text-based logins.

### NOTE

This chapter focuses on text-based logins and use of Linux. Graphical logins and using a graphical desktop are described in the section “Starting X” in Chapter 6.
