applications have gotten a bad reputation for not being stable or causing problems.
The biggest one that most people have run into is the Netscape Navigator Web
browser, but it is not the only one to blame.

Some applications just crash, while others do not actually close when told to exit.
Instead, they stay open and continue to use resources that could be better used
elsewhere. If you notice your system running slower than usual or hear the hard
drive as memory is swapped to the swap partition, you need to check your process
list. Make sure that no old applications that you thought were closed are still open
and running in the background.

![](bbox=[0.13, 0.315, 0.19, 0.36])

# Exam Tip

Many unstable applications run in X. The exam objectives specifically mention
Netscape Navigator and **tkrat** (a graphical mail agent), so you should remem-ber those.

# Running X and Clients Remotely

![](bbox=[0.12, 0.445, 0.18, 0.49])

# Objective 2.10 X

+   • Setup XDM. Turn xdm on and off, change the xdm greeting, change default bit-
+   planes for xdm, set-up xdm for use by X-stations
+   
+   • Install & Customize a **Window Manager Environment**. Select and customize
+   a system-wide default window manager and/or desktop environment, demon-
+   strate an understanding of customization procedures for window manager
+   menus, configure menus for the window manager, select and configure the
+   desired x-terminal (xterm, nvt, aterm etc.), verify and resolve library dependency
+   issues for X applications, export an X-display to a client workstation. Commands:
+   Files: .xinitrc, Xdefaults, various .rc files.

A very nice feature of X is the ability to transparently display applications across a
network. This can be used to set up inexpensive desktop computers on users`
desks, while running the applications from a large network server. X provides the
ability to either run individual client applications remotely or start the entire desk-
top from a remote system.

# Configuring X security

X supports several different authentication mechanisms, some very complex. For
most users, the basic host method works well and is easy to configure and manage.
The host-based security is configured with the `xhost` command. The current
authentication settings can be checked by just running `xhost` with no options.

```
[root@redhat /root]# xhost
access control enabled, only authorized clients can connect
INET:brain
INET:marvin
```