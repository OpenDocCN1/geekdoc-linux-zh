After you've finished making these changes, you need to restart the Samba server. If you've left the Red Hat Linux configuration as it came, you can do this by typing:

```
/etc/rc.d/init.d/smb restart
```

# Accessing Shares from Windows

There are several ways to access Samba shares from Windows, some of which are more obvious than others. Some of the most common are described in the following sections.

# Browsing a Network from Windows

Browsing the network is one of the most obvious methods of accessing Samba shares. Double-click on the Network Neighborhood icon on your desktop, and you'll get a network browser, as shown in Figure 11.5. You can double-click on a machine in this browser to see its shares, and then double-click on the shares to access the files and directories it contains, much as if it were a local hard disk.

# NOTE

> With Windows 98, you might only need to single-click to navigate through directories and files.

Accessing a share in this way can be awkward. If you regularly use a particular share, you can create a shortcut directly to it:

+   1. Open the window that shows the folder icon for the share you want to access regularly.
+   2. Right-click on this share. You get a pop-up context menu.
+   3. Select Create Shortcut. Windows displays a dialog box stating that it can't create a shortcut in that location, but that it can place one on the desktop.
+   4. Click Yes to create the shortcut on the desktop.

Thereafter, when you open the shortcut that's on the desktop, Windows opens the share, without making you go through several layers in the Network Neighborhood browser.

# Mounting a Samba Share in Windows

Browsing the network can be convenient, but sometimes you need to assign a drive letter to a share. This is true if you need to access the share by using a DOS program run under Windows, for instance, and even for some Windows programs. There are two ways to assign a drive letter to a share.