
## Chapter 4

## Using the X Window System

### In This Chapter

- The History of X 80
- Essential X Concepts 80
- Configuring XFree86 88
- Colors 97
- Fonts 98
- Starting X 101
- Some X Clients 102

The X Window system is a networked graphics system, which is the infrastructure underlying most graphical user interfaces on Linux (and indeed most UNIX systems).

## The History of X

The X Window system was first released in 1984 by the Massachusetts Institute of Technology. The first release of the current version, version 11, was released in September 1987. The most up-to-date version of X is version 11 release 6, often referred to as X11R6. (Actually, the truly latest and greatest is release 6.4, or X11R6.4.)

X was developed by MIT’s Project Athena and Digital Equipment Corporation with contributions from many other organizations and companies. Control of X passed in 1988 to the X Consortium, composed of practically all large workstation and software vendors. On December 31, 1996, all rights to the X Window system were assigned to the Open Software Foundation, which became the Open Group. On May 17, 1999, the Open Group formed a subsidiary called X.Org, which is now officially in charge of X development.

X is released under a very liberal license that not only allows free copying and use of the software but also allows it to be incorporated into commercial products with no license fee.

On Linux, the most popular X implementation is the XFree86 implementation provided by the XFree86 Project, Inc. This is a not-for-profit organization that releases X implementations for common PC video cards. The XFree86 implementation runs mostly on Intel processors, but it has been ported to all the processor architectures supported by Linux. In addition, XFree86 is the standard X server for other free UNIXes such as FreeBSD.

## Essential X Concepts

X has a number of interesting design concepts that differ from other graphical systems such as Microsoft Windows or MacOS. To fully appreciate the power of X, you must understand these differences.

### The Client/Server Nature of X

The X Window system is a client/server system. The X server controls the display on the terminal where you work. X clients send requests to the X server to draw windows, draw lines, render text, and so on. The X server sends replies back to the clients and also sends them events such as mouse motion, mouse button clicks, and key presses.

The X server is simply an ordinary Linux program. The Linux kernel knows nothing about graphics or windows; all of that is taken care of by the X server. This arrangement has an very important consequence: If, for some reason, the X server has a bug in it, which locks it up or causes it to crash, you can usually just kill it and your Linux system will remain perfectly functional.

A very powerful feature of X is that the server accepts connections from clients on the local machine or over the network. X supports a number of networking protocols, including TCP/IP, the standard Internet protocol. This means that clients can run on any machine connected to the server machine (even across the Internet) and have their windows appear seamlessly on the display. With X, the difference between local and remote programs is blurred.

This feature of X leads to the introduction of X terminals, which are simply terminals with a built-in X server and no other software. Users log in and run all their programs remotely on a (presumably powerful) central computer. The advent of cheap and powerful personal computers has rendered X servers almost irrelevant, but the powerful remote access possibilities offered by X are still very useful.

For example, suppose you have a number of servers locked away in a server room. There’s really no point in equipping each one with a keyboard and monitor, because no one ever sits in front of them. With X, you can remotely open windows on the servers and control them from your workstation, using graphical administration tools with ease.

The client/server nature of X is sometimes confusing because the server runs on the local workstation, whereas the client may run elsewhere. To reiterate:

- The X server controls the video card and performs all the drawing operations. It runs on the local workstation.
- X clients are application programs that ask the server to perform drawing operations for them. X clients can run on the local workstation or on remote machines.

### The Display

Each X server manages a display. A display refers to a keyboard, mouse, and one or more screens. (Although the X system supports multiheaded displays, the current XFree86 implementation does not. The next major release of Xfree86 (release 4.0) promises support for multiheaded displays.)

Each screen has a name that looks something like this:

```
machine:dispNum:screenNum
```

The machine is the name of the machine on which the X server is running. It might be blank if the server is running on the local machine.

The `dispNum` is a number specifying the display number.

**Background Material**

It is possible to have more than one display on a given machine. For example, under Linux, you can run two completely separate X servers in different virtual consoles. One would be display 0 and the other display 1.

The `screenNum` is the screen number. A multiheaded display can have more than one screen.

On my network, I’m running a terminal on the machine *shvey* and the X server on *shishi*. The display for the client on *shvey* is called *shishi:0.0*. You can specify the display when you start an X Client with the -display option, but usually you set the DISPLAY environment variable to the display’s name. The startup process for X automatically sets the variable correctly for local clients.

### Window Managers

Another design feature of X is that it provides mechanism, not policy. That is, the core X system provides a mechanism for drawing windows, rendering text, and handling mouse and keyboard events. It does not specify how windows should look, what a particular mouse click should do, or which keystrokes do what. For example, X does not specify which keystrokes open or close windows, minimize them, and so on.

The policy or look-and-feel of the interface is left up to the window manager. The window manager is an ordinary X client that has special powers. It draws decorative frames around windows, draws any required buttons, and provides means for users to resize, move, open, and close windows.

Figure 4.1 illustrates the X architecture. The figure shows an X server running on the local workstation. There are two local X clients connected to the server, as well as a window manager. In addition, there is a remote X client that is connected from another machine.

**FIGURE 4.1**

X Window system architecture.

![](img/df365d352a104b50fea29e59a052de4d_120_0.png)

**Background Material**

In principle, the window manager could be run remotely, but it is usually run on the same machine as the X server for performance reasons.

The separation of duties between the X server and the window manager has meant that you can try many different user interfaces. Consequently, because you can vary the look and feel simply by changing window managers without altering the core X system, it is easy to experiment with different interfaces and customize them.

**Background Material**

This is, in fact, one of the most criticized aspects of X: Because of a lack of standardization, X programs tend to have small but annoying differences in which keys are used for what operations, which mouse buttons bring up open menus, and so on.

In the commercial UNIX world, after a number of years of battles and disagreement, the Motif user interface was chosen as the standard. The Common Desktop Environment (CDE) is the standard commercial UNIX desktop.

Unfortunately, Motif and CDE are not free or open-source. For this reason, they have not found much favor on Linux, although Linux implementations are available.

For a while, Linux continued along with using many different graphical user interfaces. Eventually, two large projects emerged, promising a standardized desktop for Linux: the K Desktop Environment (KDE) and the GNU Network Object Model Environment (GNOME). Caldera chose to use KDE as the standard desktop environment for OpenLinux. KDE is covered fully in Chapter 5.
