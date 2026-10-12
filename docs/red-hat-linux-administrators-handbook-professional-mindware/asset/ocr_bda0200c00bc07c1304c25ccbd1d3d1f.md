# ## Installing Linuxconf

Installing Linuxconf is quite simple. If you did not install Linuxconf during your Red Hat Linux installation, you can install it at any time from the RPM package shipped with the official Red Hat CD-ROM. For example, I install the following RPM packages as follows:

```
rpm -ivh gnome-linuxconf-0.33-6.i386.rpm
rpm -ivh linuxconf-1.19r2-2.i386.rpm
```

The above RPM packages installs Linuxconf and the Gnome version of the Linuxconf interface.

Also, you can download the RPM package from the official Linuxconf FTP site at `ftp://ftp.solucorp.gc.ca/pub/linuxconf/devel/`.

# ## Configuring Linuxconf

Linuxconf can be used in multiple ways in either text mode, graphical mode, or web mode. It automatically chooses between the text mode (for console or remote shell) or graphics mode (for X Window). For example, if you log in to your system console and run `/bin/linuxconf` from the command line, you will see a screen similar to the one shown in Figure 4-1.

![](bbox=[0.06, 0.66, 0.94, 0.9])

Figure 4-1  The text interface for Linuxconf