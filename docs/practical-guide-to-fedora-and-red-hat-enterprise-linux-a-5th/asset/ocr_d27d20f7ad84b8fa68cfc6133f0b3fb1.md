screen (Figure 3-7, page 61), choose Use free space to have Anaconda partition the free space on the hard disk automatically. If you need to delete a Windows partition, you must choose Create custom layout; this selection calls Disk Druid (page 71) so you can delete the appropriate Windows partition and create Linux partitions in the free space. When you boot the system, you will be able to choose which operating system you want to run.

# # THE X WINDOW SYSTEM

If you specified a graphical desktop environment such as GNOME or KDE, you installed the X.org (x.org/wiki) implementation of the X Window System when you installed Linux. The X Window System release X11R7.2 comprises almost 50 software packages. The X configuration files are kept in /etc/X11.

# ## gnome-display-properties: CONFIGURES THE DISPLAY

You can use the gnome-display-properties (FEDORA) or system-config-display (RHEL) utility to display the Display Preferences window (Figure 3-27), which allows you to configure the monitor. Most users never need to run this utility. In almost all cases, Fedora/RHEL autoconfiguration sets up X.org to work properly. To run this utility, enter gnome-display-properties (FEDORA) or gnome-config-display (RHEL) on a

![](bbox=[0.34, 0.52, 0.7, 0.88])

Figure 3-27 The Display Preferences window