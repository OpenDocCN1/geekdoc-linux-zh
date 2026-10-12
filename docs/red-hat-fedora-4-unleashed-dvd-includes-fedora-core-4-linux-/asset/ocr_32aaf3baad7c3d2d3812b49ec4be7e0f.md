![](bbox=[0.14, 0.11, 0.84, 0.48])

FIGURE 21.5 Use the SWAT Shares page to set up sharing of a portion of your Linux file system.

Type the directory name (such as /music) you want to share in the Path field under the Base options. Select No or Yes in the Read Only field under Security options to allow or deny read and write access. Select Yes in the Guest OK option to allow access from other users and specify a hostname, IP address, or subnet in the Hosts Allow field to allow access. Click the Commit Changes button when finished. Remote users can then access the shared volume. This is how a Linux server running Samba can easily mimic shared volumes in a mixed computing environment!

Alternatively, use the system-config-samba client (from the command line or the Server Settings Samba Server menu item on the System Settings menu). Figure 21.6 shows the properties of a shared directory named /music. Use the Add button to create new shares and the Properties button to edit the share's access options. Use the Preferences menu to edit your Samba server's general settings or to create and manage Samba users.