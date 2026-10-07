# Remote Computer Operating

With VNC, you can sit in front of your Red Hat Linux computer and use a remote, network-connected computer running Windows or Solaris (almost any operating system), and work on that system as if you were sitting in front of it.

> > official VNC distribution does not include a PalmOS client for virtual networking. However, PalmOS PDA users can browse to http://www.harakan.btinternet.co.uk/PalmVNC/ and download-load PalmVNC. The VNC-compatible PalmOS client requires less than 40KB of memory, works like the VNC's vncviewer client, and with source code.

The Linux version of VNC includes

+   - A special X server named xvnc, used to support a background X session
- A shell script named vncserver, used to initiate the local VNC server
- A password utility named vncpassword
- A client named vncviewer, to view and run remote X sessions or desktops

Although you can download, build, and install new versions of the VNC software, you'll find nearly current copies included with Red Hat Linux.

The VNC server package must be running on a remote computer in order to view or manage the remote desktop. The vncserver script under Red Hat Linux to start a server instance using a specific geometry for the session (to offer for example, an 800x600 window session on your desktop) this:

```
$ vncserver -geometry 800x600
```

You're then asked to assign a password. After you enter the password, the session starts and Xnc reports a display number (such as :1). This password and display number are required when you or others access the session running under Red Hat Linux on your computer.

The first time you launch vncserver on your Red Hat Linux system, the software creates a vnc directory in your home directory, along with a file named xstart, and a log file using computer's hostname and X display number (such as titan.cavtel:1.log).

To access a remote desktop, use the vncviewer command, followed by the hostname (or IP address) of the remote computer, along with the Xnc session number. The session number is always 0 for Windows and 1 if an X session has already been started on a UNIX computer. For example, type the following command if you're running Red Hat Linux and would like to access a remote Linux computer running Xvc:

```
$ vncviewer marvin.cavtel:1
```