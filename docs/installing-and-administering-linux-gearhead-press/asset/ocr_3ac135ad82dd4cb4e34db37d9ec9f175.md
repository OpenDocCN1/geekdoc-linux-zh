![](bbox=[0.14, 0.08, 0.88, 0.43])

**Figure 2.19** Selecting packages to install.

+   - NFS Server
+   - Kernel development
+   - Utilities

We could have added KDE, too, at least for comparison purposes. Normally, either GNOME or KDE is installed. Support for additional features can be added after the installation by using *rpm*, the Red Hat Package Manager. All of the associated services for various run levels can be managed after the installation using either `/usr/sbin/chkconfig` or `/usr/sbin/ntsysv` to modify the services.

There is potential here for frustrating errors. For example, if you had chosen to install a GNOME Workstation, these packages would be different. You would get networking capability but you might not have Telnet or *File Transfer Protocol* (FTP) functionality, which might be important to you. Normally, you would get only Telnet, FTP, and NFS if you had chosen to do a Server installation (remember, we chose Custom). Now is your chance to add all functionalities by choosing *Select individual packages*. It is much easier to add functionalities here than to install and configure them later after the installation.

We have worked with earlier versions of Red Hat, so we were used to working with utilities such as *linuxconf* and *XFree86Config*. We consider those packages to be absolute *musts* for a system administrator. Do