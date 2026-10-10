You will be prompted to enter a password:

```
Password:
Enter a password used to allow remote access and press Enter. You will again be
asked to verify the password, like this:

Verify:
New 'X' desktop is cube:1
```

```
Creating default startup script /home/bball/.vnc/xstartup
Starting applications specified in /home/bball/.vnc/xstartup
Log file is /home/bball/.vnc/cubie:1.log
```

Note that the server returns a DISPLAY number (1 in this example). Users who wish to connect remotely will need to know this display number, along with your password in order to connect to your virtual session.

Your session settings are contained in a directory named .vnc in your home directory. The file named xstartup provides instructions on what X window manager to use for a session. You can edit this file to start any window manager you choose, like this:

```
#!/bin/sh

xrdp $HOME/.Xresources
/opt/kde2/bin/startkde
```

In this example, the K Desktop Environment is specified. When you or a remote user connects, that is the window manager in use for the session. Note that using vnc can be a resource drain; it is as if you are running another X session in memory!

Figure 17.1 shows a remote PPC Linux session (running the twm window manager) viewed from the desktop of another (Intel-based) Linux X session.

The Mac OS xvnc package also supports remote viewing. Download the Mac OS version from the xvnc home page. You will need to decompress the software. Next, double-click the VNC Server Installer script in the VNC PPC folder. The software will be installed in your System Folder, along with a VNC Controls control panel.

To enable a remote viewing session, first use the Monitors control panel to select a resolution for the Desktop. Your remote session will automatically use the size and color depth of the current Monitor's setting. Next, double-click the VNCServer PPC application and choose the Options menu item from the File menu.