# Chapter 5: Accessing and Running Applications 229

After you log in to the remote computer using ssh, you can use secure channel to forward X applications back to your local display. Here is an example:

+   1. Type the following ssh command to log in to a remote computer (the -X option enables X11 forwarding):

```
$ ssh -X jake@remotel
jake@remotel's password: ******
```

+   2. Check that the display variable is set to forward any X applications run through your ssh session to your local display (this value is controlled by the X11DisplayOffset setting in /etc/ssh/sshd_config):

```
$ echo DISPLAY
localhost:10.0
```

+   3. After you are logged in, type any X command and the window associated with that command appears on your local display. For example, to start the gedit command, type:

```
$ gedit &
```

For this work, you don't need to open your local display (using xhost). The reason this works is because the SSH daemon (sshd) on the remote system sets up a channel to your computer for X applications. So as not to interfere with any real display numbers, the SSH daemon (by default) uses the name of localhost:10.0.

This X forwarding feature is by default in the latest version of Fedora (see the X11Forwarding value set in the /etc/ssh/sshd_config file). If it is off other systems, however, you may need to change the X11Forwarding value on those systems.

# Running Microsoft Windows, DOS, and Macintosh Applications

Linux is ready to run many applications that were created specifically for Linux, the X Window System, and many UNIX systems. Other applications that were originally created for other operating systems have also been ported to Linux. However, there are still lots of applications created for other operating systems for which there are no Linux versions.

Linux can run some applications that are intended for other operating systems using emulator programs. An emulator, as the name implies, tries to act like it is not. In the case of an operating system, an emulator tries to present an environment that likes the intended operating system.

> NOTE: The most popular of these emulators, called WINE, is not an emulator at all. WINE is a mechanism that implements Windows application-programming interfaces; rather than emulating Microsoft Windows, it provides the interfaces that a Windows application would expect. In fact, some people claim WINE stands for "WINE Is Not an Emulator."