
# Remote Computer Operating

With VNC, you can sit in front of your Red Hat Linux computer and use a remote, network-connected computer running Windows or Solaris (almost any operating system), and work on that system as if you were sitting in front of it.

> The official VNC distribution does not include a PalmOS client for virtual networking. However, PalmOS PDA users can browse to http://www.harakan.btinternet.co.uk/PalmVNC/ and download-load PalmVNC. The VNC-compatible PalmOS client requires less than 40KB of memory, works like the VNC's vncviewer client, and with source code.

The Linux version of VNC includes:

- A special X server named xvnc, used to support a background X session
- A shell script named vncserver, used to initiate the local VNC server
- A password utility named vncpassword
- A client named vncviewer, to view and run remote X sessions or desktops

Although you can download, build, and install new versions of the VNC software, you'll find nearly current copies included with Red Hat Linux.

The VNC server package must be running on a remote computer in order to view or manage the remote desktop. The vncserver script under Red Hat Linux to start a server instance using a specific geometry for the session (to offer for example, an 800x600 window session on your desktop) this:

```bash
$ vncserver -geometry 800x600
```

You're then asked to assign a password. After you enter the password, the session starts and Xnc reports a display number (such as :1). This password and display number are required when you or others access the session running under Red Hat Linux on your computer.

The first time you launch vncserver on your Red Hat Linux system, the software creates a vnc directory in your home directory, along with a file named xstart, and a log file using computer's hostname and X display number (such as titan.cavtel:1.log).

To access a remote desktop, use the vncviewer command, followed by the hostname (or IP address) of the remote computer, along with the Xnc session number. The session number is always 0 for Windows and 1 if an X session has already been started on a UNIX computer. For example, type the following command if you're running Red Hat Linux and would like to access a remote Linux computer running Xvc:

```bash
$ vncviewer marvin.cavtel:1
```

After you enter a password, the vncwindow will appear with an active image of the remote desktop similar to that shown in 27.10. Once connected, you use mouse and keyboard to use applications remotely as if you were sitting in front of the remote computer. You will terminate the VNC session by closing the VNC window; VNC handles the network housekeeping on both ends of the connection.

![](img/446debe023486a07fde575245cf7a3ff_939_0.png)

**FIGURE 27.10** Use vncviewer manage remote desktops of any OS running a Linux desktop.

You can also use the vncviewer client on remote computers to view your Linux desktop, again using the assigned password and display number. By editing a simple text file, you can also craft custom sessions. The file startup under the .xinitrc directory in each user's home directory contains entries similar to what one, and can be changed to launch a specific window manager or client.

The xstartup file (actually a shell script) looks like this:

```sh
#!/bin/sh
# Red Linux VNC session startup script

exec /etc/X11/xinit/xinitrc
```

The default startup script will use Red Hat's X default settings using the window manager twm with a gray root desktop and a single xterm window. System administrators can create custom desktops for remote users.

## Cygwin for Windows

To run GNOME as the window manager in VNC (if you have the network bandwidth to spare, since VNC can use a lot of network bandwidth if linked to a graphics-intensive desktop), edit the file to look like this:

```bash
#!/bin/sh
# Red Hat Linux VNC session startup script
exec gnome-session
```

Using KDE would require a line such as

```bash
exec startkde
```

> CAUTION
> When running VNC over a public network, you are at risk because the VNC session is not encoded and passwords are passed in plain text. Advanced users familiar with ssh can use an ssh tunnel (a connection encapsulated within an ssh session) to handle the connections. You'll need to first calculate the port of the VNC server (which would be 5900 plus the display number—for a UNIX host, it would likely be 5901, for other OS hosts, probably 5900), run the VNC server with the -localhost option, and then set up ssh to forward the port to the computer running the viewer (and ssh as well).

## Other VNC-Related Applications

Because the source for VNC is openly available, there are several modifications and adaptations to the original program. Available variants provide more platform support. Here are two of the most popular variants:

- VncMonitor—A handy tool to handle the desktops of multiple computers, for monitoring multiple systems at once
- rfbplaymacro—a scripting language to enable the replay of mouse and keyboard actions, which are useful for testing and demonstrating software that lack scripting capabilities

These and other clever implementations of VNC can be found at http://www.uk.research.att/vnc/extras.html

## Cygwin for Windows

Cygwin is a Unix-like environment for the Windows/Intel architecture that is being developed by Red Hat Linux. Cygwin supports all current variants of the Windows operating system, including Windows 9X, NT, Me, 2000, and XP. The Cygwin distribution consists entirely of free, but developers might use Cygwin to create proprietary applications under a proprietary-use license available from Red Hat, Inc. You can download Cygwin from http://www.cygwin.com.

## CHAPTER 27 Using Emulators and Other Cross-Platform Tools in Red Hat Linux

You install the Cygwin distribution by downloading it and then running an installer named setup.exe. The installer then downloads and installs the portions of the Cygwin package that you indicate to install. The default installation location under Windows is C:\cywin. The Cygwin DLL works with all non-beta, x86 versions of Windows since Windows 95, with the exception of CE.

Source code for all the installed software is also available from Cygwin and you can use your existing development tools to modify existing programs or build new applications in Cygwin.

- Document and graphics utilities, such as ghostscript
- File utilities, such as bzip2, gzip
- Internet utilities, such as FTP, sftp
- Linux clients, such as ssh, scp
- Networking tools, such as curl
- Open source, such as autoconf
- Shells, such as ash, zsh
- Software libraries, such as gcc
- System scheduling, such as cron
- Text editors, such as ed, nano, vim
- Various tools, such as wget
- Window managers, such as X Window, Apache

## Cross Compilers and Other Cross-Platform Tools for Use in Linux

Cross-compilers allow you to compile win32 applications for non-Intel platforms. By taking advantage of the powerful and free tools provided in Red Hat, you can use Linux and Winelibs to develop PalmOS applications.

Winelibs is a development environment that supports the compilation of win32 applications in Linux. It allows the application to make calls directly to the Linux kernel rather than through an intermediate software layer. Win32 code written using Winibs can be recompiled with minimal code changes for a non-Intel platform.

Cross compilers for operating systems such as MS-DOS, Windows 95, NT, Mac OS (68K), OS/2, and the Amiga.

## Cross-Platform Floppy Disk Tools

There is no native, official filesystem for floppy disks for Linux. Instead, Linux uses the minix and ext2 filesystems with several others. You are more likely to encounter FAT and HFS-formatted floppy disks than any other format. Red Hat Linux provides you with a set of tools to manipulate FAT and HFS volumes (not just floppy disks) as if they were native to your computer.

# Mtools

You use Mtools to manipulate DOS volumes in Red Hat Linux. Essentially, the Mtools are Linux tools that perform functions similar to the DOS command-line tools; the tools operate in a way familiar to the DOS users. Mtools maintain DOS drive and file naming structures as arguments, so DOS users find them easy to work with.
