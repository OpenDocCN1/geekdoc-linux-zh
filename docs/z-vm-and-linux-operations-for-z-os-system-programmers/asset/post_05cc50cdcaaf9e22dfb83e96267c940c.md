
> Warning: Disabling the firewall is not a good practice. We are doing it however, to simplify our examples. Later, you should activate the firewall and block the ports for services at which you do not want your system to serve incoming connections.

The Test Internet Connection window opens.

- 7. Select No, skip this test and click Next.
- 8. In the Installation Settings window, select Skip configuration and click Next.
- 9. In the User Authentication Method window, accept the default of Local (/etc/passwd) and click Next.
- 10. In the "Add a new local user" window, you may choose to add a local user if you do not want to use the system as root every time. When you are done, click Next.
- 11. In the "Writing the system configuration" window the SUSEconfig tool writes all your settings to disk.
- 12. In the Release Notes window, review the release notes, and click Next.
- 13. In the Hardware Configuration window select Skip Configuration, and click Next.
- 14. In the Installation Completed window, if you intend to clone the system, check the box Clone This System for Autoyast, and click Finish. If you do not intend to clone the system, you may leave the check box unselected.

Congratulations! You are done installing Linux!

## 4.4.3 Logging into the Linux system

To close the installation guide in a great style, nothing is better than logging into the system you have just installed in a nice and pleasant way: Virtual Network Computing (VNC). To do that, you must have a VNC client installed on your machine. You can use Linux's vncviewer client or get one for Windows, such as RealVNC. In our examples we use RealVNC.

### Connecting to the guest using VNC

Start the RealVNC application and type in the IP address of the server (your Linux system) followed by the port number the VNC server is running on it. Figure 4-32 on page 215 shows our VNC client connecting to our Linux guest system.

Enter the VNC server information according to the IP:port format. See Figure 4-32.

![](img/b0a4b9056f819dccd4781a5105c92d45_230_0.png)

> **Note:** When you install SLES10 and enable VNC management, a VNC server will be running on port 5901 after the system boots up.

RealVNC opens a new window, which displays the X Window System. At this point, you probably do not see the KDM login manager; instead you see a blank X Window System.

To bring up the login manager, log in as root to the Linux guest through SSH and type the following text:

```
/etc/init.d/xdm start
```

Depending on your network speed, KDM can take awhile to be displayed in your current VNC display. The KDM login display is similar to the one in Figure 4-33 on page 216.

![](img/b0a4b9056f819dccd4781a5105c92d45_231_0.png)

Figure 4-33 KDM login window

Log in as root and have a first look at your graphical KDE interface.

## Configuring KDM to autostart in boot

Starting the XDM service every time you want to log into the system with VNC is not desirable. Therefore, you should enable it as a system service in the run levels.

To configure KDM to autostart, use the following steps, which correspond to the numbers in Figure 4-34 on page 217:

- 1. Click the YaST icon
- 2. Scroll down and select System in the left menu.
- 3. After the menu on the right refreshes, scroll down and select System Services (Runlevel).
- 4. Scroll down the list until you see an entry for xdm.

Figure 4-34 Enabling XDM as a system service.

- 5. Highlight the xdm line and click Expert Mode.

The window changes to an expert mode as shown in Figure 4-35 on page 218.

Figure 4-35 Runlevel editing in expert mode.

6. Enable XDM to be run on levels 2, 3 and 5. Click Finish to complete the process.

These steps should do the trick. The next time, and when you log in with a VNC client, you will see a KDM login window.

For more information about the peculiarities of a Linux installation, which we do not mention in this book, read the Gentoo handbook¹¹ at:

http://www.gentoo.org/doc/en/handbook/index.xml

¹¹ Although this is the handbook of a specific Linux distribution, the concepts behind a Linux installation are very well outlined and generic.

## System Services (Runlevel): Details

Simple Mode
Expert Mode
Set default runlevel after booting to:
3. Full multiuser with network

Assign system services to runlevels by selecting the list entry of the respective service then checking or unchecking the check boxes B-5 for the runlevel.

Start/Stop/Refresh: Use this to start or stop services individually.

Set and Reset: Select runlevels in which to run the currently selected service.

- Enable the service: Activates the service in the standard runlevels
- Disable the service: Deactivates service.
- Enable all services: Activates all services in their standard runlevels

Changes to the default runlevel will take effect next time you boot your computer.

| Service | Running | B | 0 | 1 | 2 | 3 | 5 | 6 | S | Description |
|---|---|---|---|---|---|---|---|---|---|---|
| smb | No |  |  |  |  |  |  |  |  | Samba SMB |
| smbfs | No |  |  |  |  | 3 | 5 |  |  | Import remote |
| smpppd | No |  |  |  |  |  |  |  |  | Start the smpp |
| snmpd | No |  |  |  |  |  |  |  |  | start netsnmp |
| splash | No |  |  | 1 | 2 | 3 | 5 |  | S | Splash screen |
| splash_early | Yes |  |  |  | 2 | 3 | 5 |  |  | kills animatio |
| squid | No |  |  |  |  |  |  |  |  | Squid web ca |
| sshd | Yes |  |  |  |  | 3 | 5 |  |  | Start the sshd |
| svcgssd | No |  |  |  |  |  |  |  |  | Start the RPC |
| syslog | Yes |  |  |  | 2 | 3 | 5 |  |  | Start the syste |
| vmlo... | Yes |  |  |  |  |  |  |  |  | Start the Linu |
| winbind | No |  |  |  |  |  |  |  |  | NSS daemon |
| xdm | Yes |  |  |  | 1 | 3 | 5 |  |  | X Display Ma |

X Display Manager
