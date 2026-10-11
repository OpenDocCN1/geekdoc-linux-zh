
## Graphical applications

![](img/f28adb66a7398a382f0505e0ba74a872_297_0.png)

Figure 8-1 The X stack

Computer networks are central to the design of X. It is possible to run an application on one computer and display the results on a screen attached to a different computer; the ease with which this can be done distinguishes X from other window systems available today. Thanks to this capability, a scientist can run or manipulate a program on a powerful supercomputer in another building or another country and view the results on a personal workstation or laptop computer. For more information refer to “Remote Computing and Local Displays” on page 258.

When you start an X Window System session, you set up a client/server environment. One process, called the X server, displays a desktop and windows under X. Each application program and utility that makes a request of the X server is a client of that server. Examples of X clients include xterm, Compiz, gnome-calculator, and such general applications as word processing and spreadsheet programs. A typical request from a client is to display an image or open a window.

### The roles of X client and server may be counterintuitive

**tip** The terms client and server, when referring to X, have the opposite meanings of how you might think of them intuitively: The server runs the mouse, keyboard, and display; the application program is the client.

This disparity becomes even more apparent when you run an application program on a remote system. You might think of the system running the program as the server and the system providing the display as the client, but in fact it is the other way around. With X, the system providing the display is the server, and the system running the program is the client.

**Events** The server also monitors keyboard and mouse actions (events) and passes them to the appropriate clients. For example, when you click the border of a window, the server sends this event to the window manager (client). Characters you type into a terminal emulation window are sent to that terminal emulator (client). The client takes appropriate action when it receives an event—for example, making a window active or displaying the typed character on the server.

Separating the physical control of the display (the server) from the processes needing access to the display (the client) makes it possible to run the server on one computer and the client on another computer. Most of the time, this book discusses running the X server and client applications on a single system. “Remote Computing and Local Displays” describes using X in a distributed environment.

> **optional** You can run xev (X event) by giving the command xev from a terminal emulator window and then watch the information flow from the client to the server and back again. This utility opens the Event Tester window, which has a box in it, and asks the X server to send it events each time anything happens, such as moving the mouse pointer, clicking a mouse button, moving the mouse pointer into the box, typing, or resizing the window. The xev utility displays information about each event in the window you opened it from. You can use xev as an educational tool: Start it and see how much information is processed each time you move the mouse. Close the Event Tester window to exit from xev.

## Using X

This section provides basic information about starting and configuring X from the command line. For more information see the Xserver man page and the man pages listed at the bottom of the Xserver man page.

### STARTING X FROM A CHARACTER-BASED DISPLAY

Once you have logged in on a virtual console (page 137), you can start an X Window System server by using startx. See page 423 for information on changing the initdefault entry in the /etc/inittab file that causes Linux to boot into single-user mode, where it displays a textual interface. When you run startx, the X server displays an X screen, using the first available virtual console. The following command causes startx to run in the background so you can switch back to this virtual console and give other commands:

```bash
$ startx &
```

### REMOTE COMPUTING AND LOCAL DISPLAYS

Typically the X server and the X client run on the same machine. To identify a remote X server (display) an X application (client) is to use, you can either set a global shell variable or use a command-line option. Before you can connect to a remote X server, you must turn off two security features: You must turn off the Xorg -nolisten tcp option on the server and you must run xhost on the server to give the client permission to connect to the X server. You also need to disable the firewall or open TCP port 6000 (page 824). Unless you have a reason to leave these features off, turn them back on when you finish with the examples in this section—leaving them off weakens system security. These tasks must be performed on the X server because the features protect the server. You do not have to prepare the client. The examples in this section assume the server is named tiny and the client is named dog.

### Security and the Xorg −noListen tcp option

In a production environment, if you need to place an X server and the clients on different systems, it is best to forward (tunnel) X over ssh. This setup provides a secure, encrypted connection. The method described in this section is useful on local, secure networks and for understanding how X works. See “Forwarding X11” on page 638 for information on setting up ssh so it forwards X.

### The X −noListen tcp Option

As Fedora/RHEL is installed, the X server starts with the −noListen tcp option, which protects the X server by preventing TCP connections to the X server. To connect to a remote X server, you must turn this option off on the server. To turn it off, add a DisallowTCP=false line to /etc/gdm/custom.conf following the [security] header as shown here:

```
max@tiny:~$ cat /etc/gdm/custom.conf
...
[security]
DisallowTCP=false
...
```

Reboot the system to restart the X server and gdm (gdm-binary) to make this change take effect.

### xhost GRANTS ACCESS TO A DISPLAY

As installed, xhost protects each user’s X server. A user who wants to grant access to his X server needs to run xhost. Assume Max is logged in on the system named tiny and wants to allow a user on dog to use his display (X server). Max runs the following command:

```
max@tiny:~$ xhost +dog
dog being added to access control list
max@tiny:~$ xhost
access control enabled, only authorized clients can connect
INET:dog
...
```

Without any arguments, xhost describes its state. In the preceding example, INET indicates an IPv4 connection. If Max wants to allow all systems to access his display, he can give the following command:

```
$ xhost +
access control disabled, clients can connect from any host
```

If you frequently work with other users via a network, you may find it convenient to add an xhost line to your .bash_profile file (page 281) — but see the adjacent tip regarding security and xhost. Be selective in granting access to your X display with xhost; if another system has access to your display, you may find your work frequently interrupted.

### Security and xhost

Giving a remote system access to your display using xhost means any user on the remote system can watch everything you type in a terminal emulation window, including passwords. For this reason, some software packages, such as the Tcl/Tk development system (www.tcl.tk), restrict their own capabilities when xhost permits remote access to the X server. If you are concerned about security or want to take full advantage of systems such as Tcl/Tk, you should use a safer means of granting remote access to your X session. See the xauth man page for information about a more secure replacement for xhost.

### THE DISPLAY VARIABLE

The most common method of identifying a display is to use the DISPLAY shell environment variable to hold the X server ID string. This locally unique identification string is automatically set up when the X server starts. The DISPLAY variable holds the screen number of a display:

```
$ echo $DISPLAY
:0.0
```

The format of the complete (globally unique) ID string for a display is

*[host name]:display-number:screen-number*

where *host name* is the name of the system running the X server, *display-number* is the number of the logical (physical) display (0 unless multiple monitors or graphical terminals are attached to the system, or if you are running X over ssh), and *screen-number* is the logical number of the (virtual) terminal (0 unless you are running multiple instances of X). When you are working with a single physical screen, you can shorten the identification string. For example, you can use *tiny:0.0* or *tiny:0* to identify the only physical display on the system named *tiny*. When the X server and the X clients are running on the same system, you can shorten this identification string even further to :0.0 or :0. An ssh connection shows DISPLAY as localhost:10.0. You may have to use ssh -X to set this value. See “X11 forwarding” on page 622 for information on setting up ssh so that it forwards X.

If DISPLAY is empty or not set, the screen you are working from is not running X. An application (the X client) uses the value of the DISPLAY variable to determine which display, keyboard, and mouse (collectively, the X server) to use. One way to run an X application, such as gnome-calculator, on the local system but have it use the X display on a remote system is to change the value of the DISPLAY variable on the client system so it identifies the remote X server.

```
sam@dog:~$ export DISPLAY=tiny:0.0
sam@dog:~$ gnome-calculator &
```

The preceding example shows Sam running gnome-calculator with the default X server running on the system named tiny. After setting the DISPLAY variable to the ID of the tiny server, all X programs (clients) Sam starts use tiny as their server (i.e., output appears on tiny’s display and input comes from tiny’s keyboard and mouse). Try running xterm in place of gnome-calculator and see which keyboard it accepts input from. If this example generates an error, refer back to the two preceding sections, which explain how to set up the server to allow a remote system to connect to it.
