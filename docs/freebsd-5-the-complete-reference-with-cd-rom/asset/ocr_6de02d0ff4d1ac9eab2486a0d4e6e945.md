TCP Wrappers configuration files. This section covers a few other important configuration files. These include

+   * **/etc/crontab**
+   FreeBSD ships with a utility called `crontab` that’s used to run programs at scheduled times. These *cron jobs*, as they’re called, enable you to configure the system to automatically perform routine maintenance tasks, as described in Chapter 28. The `/etc/crontab` file controls the system cron jobs. Its format is described in Chapter 6.

+   * **/etc/dhclient.conf**
+   Some computers use the Dynamic Host Configuration Protocol (DHCP) client program, `dhclient`, to automatically obtain an IP address and associated network information from a DHCP server. The `dhclient` configuration file is `/etc/dhclient.conf`. It can usually be left alone, but you may need to set options in this file on some networks. Chapter 14 covers this topic.

+   * **/etc/fstab**
+   This file is critically important for partition and filesystem management. The name is short for *filesystem table*; the file contains information on partitions, the filesystems they use, and where they should be mounted in FreeBSD’s directory tree. Chapter 7 covers this topic in more detail.

+   * **/etc/printcap**
+   FreeBSD’s printer handling relies upon a *printer capabilities* file, called `/etc/printcap`. This file lists printers, what hardware or remote computers FreeBSD uses to connect to them, what software FreeBSD uses to process files sent to them, and so on. Chapter 7 covers this topic in more detail.

+   * **/etc/resolv.conf**
+   This file tells FreeBSD what name servers to use to convert Internet hostnames into IP addresses. Chapter 14 describes this file in more detail.

+   * **User and group files**
+   The `/etc/passwd`, `/etc/master.passwd`, and `/etc/group` files hold information on user accounts and groups. You edit one or more of these files when making changes to user accounts, as described in Chapter 10. (It’s often desirable to use specialized tools to make these changes, rather than editing the files directly with a text editor.)

As with other configuration file lists in this chapter, this list is not complete. Some of these files might not be present or might not be used on your system, but most of them are present on most systems. Additional files may be important for particular configurations.

# An Overview of FreeBSD Text Editors

Before you can edit configuration files to get your system working the way you want it to work, you must be able to edit files in general. This section therefore describes some of FreeBSD’s text editor options, including sample sessions with two editors.