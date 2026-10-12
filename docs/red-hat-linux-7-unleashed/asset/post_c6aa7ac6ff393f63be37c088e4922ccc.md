
+ Solaris 2.5 (SPARC)
+ Win32 (such as Windows 9x/2000/NT)
+ Windows CE2 (for the SH3 and MIPS processors)

The latest version of this software is available at http://www.uk.research.att.com/vnc. A compressed archive of binaries for Linux is available, and you can download the 2.5MB UNIX source code tarball.

## Building and Installing the vnc Software

This section details how to download and install the vnc software. If you download the binaries, decompress the file with the tar command:

```
# tar xvfz vnc-3.3.3r1_x86_linux_2.0.tgz
```

This creates a vnc_x86_linux_2.0 directory. Read the included README file in the directory, and copy the files Xvnc, vncserver, vncviewer, and vncpasswd to the /usr/local/bin directory. If you install the vnc software from your Red Hat Linux CD-ROMs, you'll find the command under the /usr/bin directory. If you download the vnc source, decompress the archive with the tar command:

```
# tar xvfz vnc-3.3.3r1_unixsrc.tgz
```

This creates the vnc_unixsrc directory. Navigate into the directory and then start the build with the xmkmf command:

### Note

The xmkmf command (actually a shell script) is installed from your CD-ROM when you install development software for the X Window System. You'll find xmkmf, along with other software tools such as lmake, in the XFree86 RPM development archive. For more information about xmkmf, see Chapter 24, "Linux C/C++ Programming Tools."

```
# xmkmf
# make World
```

Navigate into the Xvnc directory and build the vnc X server like this:

```
# cd Xvnc
# make World
```

Finally, install the vnc software (as root) with the included installation script, specifying an installation directory:

```
# ./vncinstall /usr/local/bin
```

This completes your Linux software installation. However, if you want to work on the desktops of other computers, you need to download and install the vnc software for the desired platform. For example, if you want to work with a Windows 95 or Windows 98 desktop, download the Win32 vnc software onto the desired computer.

## Enabling Virtual Network Service

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

**FIGURE 28.11**
The Win32 vnc software provides easy-to-use dialogs and menus you can use to offer remote operation via your network.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_957_0.png)

## Viewing Remote Desktops

To view the remote Win32 desktop from Linux, use the vncviewer command, followed by the hostname or IP address of the Win32 computer. Type the command in an X11 terminal window like this:

```
# vncviewer thinkpad.home.org:0
```

You are prompted for the password of the remote vnc server:

```
vncviewer: VNC server supports protocol version 3.3 (viewer 3.3)
Password:
```

After you type in the password and press Enter, an X11 window appears with the remote desktop (as shown in Figure 28.12). You can then launch remote applications and work on the computer as if it were your own!

### Note

The vncviewer client and vncserver script also recognize several X11 Toolkit options, such as geometry settings. For example, if you start the vncserver on a remote Linux computer (such as through a Telnet session), you can specify the size of remotely viewed desktops with the geometry option, followed by the size of the desktop in horizontal and vertical pixels. To start an 800×600-pixel server desktop, use vncserver like this:

```
# vncserver -geometry 800x600 hostname:displaynumber
```

When this desktop is viewed remotely from another computer, the desktop will use an 800×600 display. (The default size of a vnc desktop is 1,024×768 pixels.)

For more information about X11 Toolkit options, see the X man page.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_958_0.png)

You can also use the vncviewer client on remote computers to view the Linux desktop. The settings and X resource files for the Linux vnc desktop may be quite different from your normal X session! Look in the `.vnc` directory for the file `xstartup`, which will look like this:

```
#!/bin/sh

xrdb $HOME/.Xresources
xsetroot -solid grey
xterm -geometry 80x24+10+10 -ls -title "VNCDESKTOP Desktop" &
twm &
```

Note that only a single X terminal and this twm window manager are used! Edit this file to suit your needs. Of course, with all this flexibility, remote sessions can get a little confusing. For example, Figure 28.13 shows a remote computer using KDE for its X11 session; this session is being viewed by a Windows 98 desktop, which in turn is being remotely viewed through a Red Hat Linux GNOME Enlightenment X session!

# PART IV

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_959_0.png)

A chain of three remote virtual network sessions can get a bit confusing, but works quite well thanks to the vnc software.

## Summary

This chapter introduced you to a number of useful software tools that can be used to extend the Linux computing experience. Emulators or virtual networks can be used to add flexibility to your computing environment or to breathe new life into legacy operating systems and applications. As you can see, there are quite a few programs and suites of software available for Linux that interact and work with Apple Computer's MacOS and Microsoft's Windows operating systems. You'll also find a host of software tools that make life a lot easier when dealing with removable media (such as floppies) for other operating systems. It is up to you to explore the networking limits of these applications or to find new uses for older software through emulators.

# Appendixes

# PART V

## In This Part

- A The Linux Documentation Project 925
- B Top Linux Commands and Utilities 931
- C The GNU General Public License 973
- D Red Hat Linux RPM Package Listings 983

# The Linux Documentation Project

## APPENDIX A

### IN THIS APPENDIX

- 1. Overview of The Linux Documentation Project 926
- 2. Current Projects and Getting Involved 927
- 3. LDP Websites 927
- 4. Documentation Conventions 927
- 5. LICENSE REQUIREMENTS 928
- 6. Boilerplate License 928
- 7. Publishing LDP Documents 929

### Note

According to Matt Welsh, the original maintainer of the LDP Web pages, LDP authors “wishing to send new or updated HOWTOs” (and other documentation) should send them to:

`ldp-submit@lists.linuxdoc.org`

There are also, according to Welsh, several mailing lists of interest about LDP. For general discussion concerning the LDP:

`ldp-discuss@lists.linuxdoc.org`

An announcement list concerning new LDP documents:

`ldp-announce@lists.linuxdoc.org`

An LDP author discussion list concerning the DocBook (SGML) format:

`ldp-docbook@lists.linuxdoc.org`

Authors or interested parties can subscribe to the lists by sending mail with the Subject: “subscribe” to:

`list-name-REQUEST@lists.linuxdoc.org`

For the latest information regarding the LDP, browse to:

`http://www.linuxdoc.org`

Revised by: David S. Lawyer (dave@lafn.org)

Last Revision: 18 July 2000

Describes the goals, status, documentation conventions, and license requirements of the Linux Documentation Project.

## 1. Overview of The Linux Documentation Project

The Linux Documentation Project is working on developing free, high quality documentation for the GNU/Linux operating system. The overall goal of the LDP is to collaborate in all of the issues of Linux documentation. This includes the creation of “HOWTOs” and “Guides”. We hope to establish a system of documentation for Linux that will be easy to use and search. This includes the integration of the manual pages, info docs, HOWTOs, and other documents.
