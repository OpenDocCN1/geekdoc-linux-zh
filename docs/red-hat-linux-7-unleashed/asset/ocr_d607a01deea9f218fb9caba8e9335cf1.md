Finally, install the vnc software (as root) with the included installation script, specifying an installation directory:

```
# . /vncinstall /usr/local/bin
```

This completes your Linux software installation. However, if you want to work on the desktops of other computers, you need to download and install the vnc software for the desired platform. For example, if you want to work with a Windows 95 or Windows 98 desktop, download the Win32 vnc software onto the desired computer.

# Enabling Virtual Network Service

The vnc server software must be started on a remote computer in order to work on the remote computer’s desktop. Under Linux, this may be done through a Telnet session or by sitting at the console and starting the software.

To start the server for Linux, use the vncserver script from the command line:

```
# vncserver
You will require a password to access your desktops.

Password:
```

Enter a password used to allow remote access and press Enter. The script then loads and starts the Xvnc X11 server (a customized X11R6.3 server based on XFree86 3.3.2).

In order to start the vnc server software on a remote Windows computer, the vnc software for Win32 must be downloaded and copied onto the remote Windows computer. The Win32 software must then be extracted with an archive utility such as WinZip.

Decompress the Win32 vnc software and install the software with the vnc Setup. You can run Win32 vnc software as a server or as a program. To start the server, click the Install Default Registry Settings menu item from the vnc folder on your desktop’s Start menu, then click the Install WinVNC Service menu item.

If you run WinVNC as a program, click the Run WinVNC (App Mode) menu item. You’ll see a dialog, as shown in Figure 28.11.

Enter a password in the dialog, and click OK. If you need to customize your settings or change the password for access to the Win32 desktop, click the WinVNC settings menu item. That’s all there is to do! From another computer on the network, use the vncviewer command, along with the server Display Number (default of 0 for Win32) and password to log in to your computer.