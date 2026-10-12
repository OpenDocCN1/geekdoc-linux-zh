+   2.  Click New to create a new Samba share.
+   3.  Choose a directory either by typing the path into the appropriate text widget, or use the Browse button to select it.
+   4.  Type a description of the share into the indicated text widget.
+   5.  Choose whether or not to allow write access to this share by selecting the corresponding radio button.
+   6.  Click OK when you’re finished.

# Project Summary

You can change any of the options you just set by selecting the share and clicking the Properties button. In addition, in the Preferences menu you’ll find the options to change broader properties of your Samba server, such as your workgroup name. Although this tool doesn’t have quite the variety of options that SWAT provides, it is effective in quickly and easily setting up a share.

# Using smbclient

The **smbclient** program is a command-line tool that allows your Linux system to act as a Windows client. You can use this utility to connect to other Samba servers or even to real Windows NT/2000 servers. The **smbclient** program is very flexible and can be used to browse other servers, send and retrieve files from them, or even print to them. As you can imagine, this is also a great debugging tool since you can quickly and easily check whether a new Samba installation works correctly without having to find a Windows client to test it.

In this section, we’ll show you how to do basic browsing, remote file access, and remote printer access with **smbclient**. However, remember that **smbclient** is a very flexible program, limited only by your imagination.

# Browsing a Server

With so many graphical interfaces around, we’ve come to equate browsing to mean “point and click.” But when your intention is to simply find out what a server has to offer, it’s not enough of a reason in itself to support an entire GUI.

Using **smbclient** with the `-L` option allows you to view the offerings of an NT or Samba server without having to use a GUI. Here’s the format of the command:

```
```bash
[root@pcard root]# smbclient -L hostname
```
```