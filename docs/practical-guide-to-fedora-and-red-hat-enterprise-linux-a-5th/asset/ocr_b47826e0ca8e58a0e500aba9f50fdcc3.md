command line or select **Main menu: System\u2195Preferences\u2195Display** (*Fedora*) or **Main menu: System\u2195Administration\u2195Display** (*RHEL*).

Figure 3-27 shows the Display Preferences window, which allows you to specify the resolution for the monitor. Normally the system probes the monitor and fills in these values. If these values are missing, check the specifications for the monitor and select the appropriate values from the drop-down lists.

# ## MORE INFORMATION

*Web* X.org: www.x.org/wiki, www.freedesktop.org

X.org FAQ: www.x.org/wiki/FAQ

# # CHAPTER SUMMARY

Most installations of Fedora/RHEL begin by booting from the live CD or the install DVD. When the system boots from the CD/DVD, it displays a message saying when it will boot automatically. During the time it displays this message, you can give various commands and then have the system continue booting.

The program that installs Fedora/RHEL is named Anaconda. Anaconda identifies the hardware, builds the necessary filesystems, and installs or upgrades the Fedora/RHEL operating system. It can run in textual or graphical (default) interactive mode or in batch mode using Kickstart.

The **Disk Druid** graphical disk-partitioning program can add, delete, and modify partitions and logical volumes (LVs) on a hard disk during installation. The **partmpset** utility reports on and manipulates hard disk partitions before or after installation. The **system-config-lvm** utility works with logical volumes after installation.

A dual-boot system can boot one of two or more operating systems, frequently Windows and Linux. The biggest task in setting up a dual-boot system, assuming you want to add Linux to a Windows system, is finding enough disk space to hold Linux.

Fedora/RHEL uses the X.org X Window System version X11R7.2. Fedora/RHEL uses the GNOME display manager (**gdm**) to provide a graphical login.

# EXERCISES

+   1. What is a live system? What advantages does it have over an installed system?
+   2. Which boot parameter would you use to begin an FTP installation?
+   3. Describe the Anaconda installer.