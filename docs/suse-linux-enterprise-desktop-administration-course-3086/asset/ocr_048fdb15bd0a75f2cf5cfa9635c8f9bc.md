This section contains the following information:

+   - Understanding the Novell Client for Linux Virtual File System
+   - Configuring the Novell Client for Linux
+   - Using Configuration Files to Preconfigure the Novell Client

# Understanding the Novell Client for Linux Virtual File System

The Novell Client for Linux has a Virtual File System that consists of a kernel module (`novfs.ko`) that runs as part of the Linux kernel and a daemon (`novfsd`) that runs in the user space. Both components must be running on the workstation for the client to connect to the network.

# Using the Novell Client Tray Application

You can use the Novell Client tray application to access many of the Novell Client for Linux features. Simply click the red N icon (▣) located in the tray.

This section contains the following information:

+   - Starting and Stopping the Novell Client Tray Application
+   - Logging In to the Network
+   - Logging Out of a Network Location (Server or Tree)
+   - Viewing Your Network Connections

# Starting and Stopping the Novell Client Tray Application

Select ▣ to see the menu shown in Figure 13-17.

![](bbox=[0.0877, 0.5185, 0.397, 0.707])

Figure 13-17

If you want to stop the Novell Client tray application from appearing on the tray, select ▣ > Quit.

To restart the Novell Client tray application (or if for some reason the red N icon (▣) does not appear in your tray), use one of the following methods:

+   - **GNOME:** Select Computer > More Applications > Novell Tray.
+   - **KDE:** Select KDE menu > Novell Tray.
+   - Enter the following command in a terminal window:

```
```bash
/opt/novell/ncl/bin/ncl_tray
```
```