+   * `fstab` — Identifies the devices for common storage media (hard disk, floppy, CD-ROM, etc.) and locations where they are mounted in the Linux system. This is used by the `mount` command to choose which file systems to mount.
+   * `group` — Identifies group names and group IDs (GIDs) that are defined on the systems. Group permissions in Red Hat Linux are defined by the second of three sets of `rwx` (read, write, execute) bits associated with each file and directory.
+   * `host.conf` — Sets the locations in which domain names (e.g., `redhat.com`) are searched for on `TCP/IP` networks (such as the Internet). By default, the local hosts file is searched, then any nameserver entries in `resolv.conf`.
+   * `hosts` — Contains IP addresses and host names that you can reach from your computer. (Usually this file is used just to store names of computers on your LAN or small private network.)
+   * `hosts.allow` — Lists host computers that are allowed to use certain `TCP/IP` services from the local computer.
+   * `hosts.deny` — Lists host computers that are *not* allowed to use certain `TCP/IP` services from the local computer.
+   * `xinetd.conf` — Contains simple configuration information used by the `xinetd` daemon process. This file mostly points to the `/etc/xinetd.d` directory for information about individual services (described later).
+   * `info-dir` — Contains the top heading for information that is available from the `info` command.
+   * `initab` — Contains information that defines which programs start and stop when Red Hat Linux boots, shuts down, or goes into different states in between. This is the most basic configuration file for starting Linux.
+   * `issue` — Contains the lines that are displayed when a terminal is ready to let you log in to Red Hat Linux from a local terminal, or the console in text mode.
+   * `issue.net` — Contains login lines that are displayed to users that try to log in to the Linux system from a computer on the network using the `telnet` service.
+   * `lilo.conf` — Sets various parameters used by the Linux boot loader (`lilo`) to boot your Linux system. In particular, it lists information about the bootable partitions on your computer. (If you are using `grub`, which has replaced `lilo` as the default boot manager, the `lilo.conf` file is not used.)
+   * `mail.rc` — Sets system-wide parameters associated with using mail.
+   * `man.config` — Used by the `man` command to determine the default path to the location of man pages.
+   * `modules.conf` — Contains aliases and options related to loadable kernel modules used by your computer.
+   * `mtab` — Contains a list of file systems that are currently mounted.