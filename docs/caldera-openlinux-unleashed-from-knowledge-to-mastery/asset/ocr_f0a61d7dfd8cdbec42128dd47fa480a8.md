# ## Introduction to the NetWare Client for Linux

The NetWare client component of Caldera OpenLinux lets you seamlessly integrate your Linux installation into your organization’s existing NetWare environment. The client provides full functionality for communicating with NetWare 3.x and 4.x servers. Specifically, it provides the following services:

+   - Recognition of all NDS trees and bindery servers on the network
+   - Utilities for logging in and out of NDS trees and bindery servers
+   - Mounting of all accessible NDS objects and files upon NDS login
+   - Printing and print queue management utilities
+   - NetWare broadcast message utilities
+   - Other utilities for managing user passwords, mount points, and so forth

# # Getting Started with the NetWare Client

This section will explain how to get started with NetWare. That is, how to install, configure, and perform other basic tasks.

# ## Installing the NetWare Client and Utilities

To install the NetWare client, Internetwork Packet Exchange (IPX) must be either compiled into the kernel or loaded as a module. Load as Module is the default of a Caldera OpenLinux installation, and unless you have changed it, your system should be ready to install the client packages and utilities.

To install the NetWare client, you must execute the following series of commands as user root, with the floppy (which comes with your Caldera OpenLinux distribution) inserted in the floppy drive:

```
```
mount -t ext2 /dev/fd0 /mnt/floppy
rpm -ivh /mnt/floppy/nwclient-4.2.0_c0122-1.i386.rpm
```
```

Once installed, the NetWare client automatically starts each time you reboot your system. If you want to start it immediately without rebooting, enter the following command:

```
```
/etc/rc.d/init.d/nwclient
```
```