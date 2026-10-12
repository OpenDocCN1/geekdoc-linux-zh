+   * /home — Because your user account directories are located in this directory, having a separate /home account can prevent an indiscriminate user from filling up the entire hard disk. (Disk quotas, see Chapter 10, represent another way of controlling disk use.)
+   * /tmp — Protecting /tmp from the rest of the hard disk by placing it on a separate partition can ensure that applications that need to write to temporary files in /tmp are able to complete their processing, even if the rest of the disk fills up.

Although people who use Red Hat Linux casually rarely see a need for lots of partitions, those who maintain and occasionally have to recover large systems are thankful when the system they need to fix has several partitions. Multiple partitions can localize deliberate damage (such as denial-of-service attacks), problems from errant users, and accidental file system corruption.

# Reclaiming disk space from existing partitions

Chances are that your PC came with a Windows operating system already installed on the entire disk. Installing Red Hat while keeping Windows on your hard disk presents a problem. Red Hat Linux and Windows operating systems are put on separate disk partitions, and right now there is only one partition (and it isn't for Red Hat Linux).

If you are in this predicament, but you have a lot of unused space in your Windows partition (at least 1GB or more), follow this procedure to reclaim the disk space.

> **CROSS-REFERENCE:** If, instead of adding Linux to an existing Windows computer, you want to add Windows to your Linux computer, refer to the Linux+Windows+Grub HOWTO. For information on installing Windows NT and Linux on the same computer, refer to the Linux+Windows NT mini-HOWTO. These and other Linux HOWTOs are available from the Linux Documentation Project (`www.tldp.org`).

# Before you begin

Read this section before you begin resizing your Windows partitions!

FIPS is a well-tested utility for resizing DOS FAT and VFAT file systems so that space can be made available to install Linux. To find out what kind of file system is being used on your Windows computer, do the following while Windows is running:

+   1. Double-click the My Computer icon.
+   2. Right-click the hard-disk (C:) icon and select Properties.
+   3. Look at the File system line. If it shows the file system type as FAT or FAT32 the disk partition can be resized with FIPS.

If you are using a Windows 95, Windows 98, or Windows ME computer, providing that you have enough free disk space on the partition, you can probably use FIPS to resize it. If, however, you have a Windows 2000, Windows NT, or Windows XP computer with an NTFS file system, you will have to use some other tools to resize it. Here are some of your choices: