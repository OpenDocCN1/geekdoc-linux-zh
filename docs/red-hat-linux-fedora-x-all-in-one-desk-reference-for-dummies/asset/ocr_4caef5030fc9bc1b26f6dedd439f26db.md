# Using the NFS Server Configuration tool

Fedora Core comes with a graphical NFS Server Configuration tool that makes configuring and starting the NFS server easy. To configure the NFS server using this tool, follow these steps:

+   1. Log in as root and choose Main Menu: System Settings->Settings:NFS from the GNOME or KDE desktop.

The NFS Server Configuration window appears.

+   2. Click Add to the toolbar.

The Add NFS Share dialog box appears.

+   3. Add the directories you want to share via NFS.

Start by specifying the directory, which has access to it (the hosts or IP addresses), and what type of access (read-only or read-write). Figure 6-1 shows the settings for the /home directory being shared with read-write access all hosts in the 192.168.0.0 network.

![](bbox=[0.136, 0.642, 0.213, 0.783])

![](bbox=[0.216, 0.457, 0.693, 0.793])

+   4. Click the General Options tab in the Add NFS Share dialog box and set the options you want (as shown in Figure 6-2).

These options correspond to the options listed in the General Options section of Table 6-1.