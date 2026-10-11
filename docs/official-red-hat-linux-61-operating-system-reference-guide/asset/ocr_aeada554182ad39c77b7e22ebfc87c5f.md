# Please Note

If you are upgrading your Red Hat Linux system to Red Hat Linux 6.2, any changes you have made to files in `/etc/sysconfig` will be migrated to `/etc/sysctl.conf`. You should confirm this by reviewing the file.

# Linux 2.2.14 kernel:

Red Hat Linux 6.2 includes the latest stable version of the 2.2.x Linux kernel.

# service now run as daemon:

The ident service is now run as a stand-alone service (called "identd"), and is controlled by settings in the `/etc/identd.conf` file.

# Workstation-class installation now more secure:

Workstation-class installations no longer install the inetd "super server." This means that the following network-related services will not be available if you perform a workstation-class installation:

+   * ftp
+   * telnet
+   * shell
+   * login
+   * talk
+   * finger

If you require the above network-related services, you should consider an installation type other than workstation-class.

# XFree86 version 3.3.6: