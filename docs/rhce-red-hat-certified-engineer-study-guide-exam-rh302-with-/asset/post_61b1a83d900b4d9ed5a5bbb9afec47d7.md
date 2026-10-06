
# Logging In Remotely

To log in to a host running an X display manager, issue a command of the form

```
X query server
```

where server is the host name or IP address of the host running the display manager. To log in to an arbitrary host on the local network, issue the command

```
X -broadcast
```

Some hosts are configured to provide a chooser, a special menu that lets you select the host you want to log in to. Figure 28.3 shows a typical chooser. To request a chooser, issue a command of the form

```
X -indirect
```

where server is the host name or IP address of the host configured to provide a chooser.

## FIGURE 28.3 A Chooser

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_691_0.png)

# Choosing a Display Manager

As explained in Chapter 27, "Understanding and Using Window Managers and Desktops," Red Hat Linux lets you choose one of three X display managers:

- XDM, the display manager distributed by XFree86 Project
- GDM, the display manager distributed with GNOME
- KDM, the display manager distributed with KDE

If you want to be able to provide a chooser, you should configure XDM as the preferred display manager; both GDM and KDM have some peculiarities that limit their ability to work with choosers. For example, GDM doesn't respond to chooser messages and therefore won't appear on the chooser menu. The KDM display manager responds to chooser messages, but sometimes not provide a chooser.

# Configuring xdm to Provide a Chooser

To configure XDM to provide a chooser, you must modify the xdm configuration file, /etc/X11/xdm/Xaccess, by adding one or more chooser directives. These directives have the following format:

```
client CHOOSER server_list
```

where chooser specifies the clients to whom a chooser will be provided, and server_list specifies the servers that will appear in the chooser. The client hosts can be specified using wildcards. The following example configuration:

```
workstation CHOOSER server1 server2
*.azusaspacific.com CHOOSER server3
* CHOOSER server4
```

The first line specifies that the host workstation will be provided a chooser that shows server1 and server2. The second line specifies that all hosts in the azusaspacific.com domain will be provided a chooser that shows server3. The final line specifies that all hosts will be provided a chooser that shows host server4. If the name of a host has several CHOOSER lines, the line appearing first is used. In the example configuration, the host workstation.azusaspacific.com would be provided a chooser that shows server1 and server2 even though the host name lines 2 and 3 as well as line 1.

# Configuring Remote Login

You can specify the list of servers dynamically by using the keyword BROADCAST. For example, consider the following directive:

```
* CHOOSER BROADCAST
```

The BROADCAST keyword causes the display manager to assemble a list of X servers on the local network by sending a special broadcast message. All servers that respond to the broadcast message will be included in the chooser.

By default, XDM ignores chooser requests. To configure XDM to respond, you must comment or remove the last line in /etc/X11/xdm/xdm-config:

```
DisplayManager.requestPort: 0
```

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_693_0.png)

> If you prefer to use KDM as a display manager and want to provide a chooser, you can configure KDM using the same procedure used for XDM. To configure gdm to provide a chooser, you must set Enable=1 in the [dmcp] section of the /etc/X11/gdm/gdm.conf and force gdm to reread the file by issuing the command killall -HUP gdm.

Now, complete Exercise 28.2 to gain experience configuring remote logins.

# EXERCISE 28.2

# Configuring Remote Logins

To practice configuring remote X logins, perform the following steps:

- 1. On a server, configure XDM as the preferred display manager and configure XDM to provide a chooser to any host on the local network.
- 2. From a client host, log in to the server by means of the chooser. What happens?
- 3. On a server, configure GDM as the preferred display manager.
- 4. From a client host, attempt to log in to the server by means of the chooser. What happens?
- 5. On a server, configure KDM as the preferred display manager.
- 6. From a client host, attempt to log in to the server by means of the chooser. What happens?

You can consult this book and other documentation to help you complete this exercise. But, before taking the RHCE exam, be sure you can perform operations such as these without help.

# The Xnest Program

Sometimes it's useful to run multiple X servers on a single host that has only a single video adapter. For example, you may want to test a new window manager or log in via X to a remote server while already running a local X server. The Xnest program provides an X server that runs in window owned by the currently running X server. You can run multiple instances of Xnest and use each X server it provides just as you would an ordinary X server. For example, to create a second X server using Xnest, issue the following command:

```
Xnest :1 &
```

Similarly, to create a third X server using Xnest, issue the following command:

```
Xnest :2 &
```

To create a second X server and use it to log in to a specified host, issue a command of the form

```
Xnest -query server :1 &
```

where server is the host name or IP address of the host you want to log in to. Similarly, you can use Xnest to log in to an arbitrary host or to obtain a chooser:

```
Xnest -broadcast :1 &          # log in to any host on the local network
Xnest -indirect server :1 & # log in via chooser provided by server
```

Copyright©2000 SYBEX, Inc., Alameda, CA

www.sysex.com

Xnest will fail unless both the Xnest and the remote system have identical fonts. This significantly limits the applicability of Xnest. Now complete Exercises 28.3 and 28.4 to gain experience.

# EXERCISE 28.3

# Using Xnest

One common use of Xnest is to run multiple X servers on a single host. Try this firsthand by using Xnest to Perform these steps:

- 1. Start an X session, and then use Xnest to create a X server on the same host.
- 2. Launch an X client—such as xeyes—that uses the second server.

You can consult this book and other documentation to help you complete this exercise. But, before taking the RHCE exam, be sure you can configure Xnest without help.

# EXERCISE 28.4

# Running Multiple Window Managers

Another common use of Xnest is to run multiple desktop managers on a single host. Try this firsthand by using Xnest to run GNOME and KDE simultaneously.

# X Font Server

By default, each system configured to run Red Hat Linux runs its own copy of the font server, xfs, which provides access to locally stored fonts. However, you can reconfigure a system to access a remote font server, if you prefer.

To do so, modify the FontPath directive of the /etc/X11/X86Config file each system. By default, the directive has this:

```
FontPath "unix:-1"
```

To access a remote font server, revise the directive to have the form:

```
FontPath "tcp/server:7100"
```

where server is the host name or IP address of the host running the server. You must also modify the /etc/rc.d/init.d/xfs file. Change the line

```
daemon xfs -droppiv -port -1
```

to read

```
daemon xfs -droppiv -port 7100
```

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_696_0.png)

By default, an X font server listens on port 7100. However, you can assign another port, if you prefer. To do so, modify the font server configuration file, /etc/X11/fs/config, and the font server SysVinit file, /etc/rc.d/init.d/xfs. See the xfs page for details.

Now, configure a remote font server by completing Exercise 28.5.

> EXERCISE 28.5
 Configuring a Client to Use a Remote X Font Server

To test your understanding of xfs, configure a client host to use the X font server running on a remote server.

You can consult this book and other documentation to help you complete this exercise. But, before taking the RHCE exam, be sure you can configure a remote X font server without help.

# Summary

In this chapter, you learned about configuring and using remote X servers and clients. The most important topics covered are:

- X Security X implements a simple host-based security system. You can configure which hosts are allowed to access an X server by using the host command.
- Remote X Clients The DISPLAY environment variable specifies the X server, which can reside on a remote host.
