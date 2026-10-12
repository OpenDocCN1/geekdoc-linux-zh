# Using the Red Hat NFS Server Configuration tool

Red Hat Linux comes with a graphical NFS Server Configuration tool that makes it easy to configure and start the NFS server. To configure the NFS server using this tool, follow these steps:

+   1. **Log in as root and choose Main Menu:System Settings:Server Settings:NFS Server from the GNOME or KDE desktop.**
+      The NFS Server Configuration window appears.
+   2. **Click Add on the toolbar.**
+      The Add NFS Share dialog box appears.
+   3. **Use the dialog box to add directories you want to share via NFS.**
+      Start by specifying the directory, who has access to it (the hosts or IP addresses), and what type of access (read-only or read-write). Figure 6-1 shows the settings for /home directory being shared read-write with all hosts in the 192.168.0.0 network.

![](bbox=[0.22, 0.55, 0.78, 0.8])

Figure 6-1:
Specify the share directory and basic permissions from this dialog box.

4. **Click the General Options tab in the Add NFS Share dialog box and set the options you want (as shown in Figure 6-2).**
These options correspond to the options listed in the General Options section of Table 6-1.