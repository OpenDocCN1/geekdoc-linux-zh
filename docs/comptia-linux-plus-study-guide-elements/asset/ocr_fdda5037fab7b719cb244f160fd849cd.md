for a file called *xdmrc*. Look for the [Xdmcp] section of this file and be sure the Enable option is set to true.

GDM completely abandons the XDM style of configuring remote logins. Instead, you should look for a file called *gdm.conf* or *custm.conf*, which is likely to be located in /etc/X11/gdm or /etc/gdm. Look for a section called [xdmcp] and be sure the Enable option is set to true.

> **TIP** Most Linux distributions have been taking extra steps in recent years to secure their default configurations. These steps may include setting firewall rules to block access to the XDMCP port, so if you have problems getting a newly configured XDMCP server to respond, you should check your firewall rules.

# ## Using an X Server

To use X to connect to a remote X server, you must alter the way X starts up. An easy way to test the configuration is to shut down the X server on the desktop system, log in using text mode, and then start X manually. A command such as the following should connect to a remote XDMCP server and permit a login:

```
`$ Xorg -query zeus.example.com`
```

This command starts X and tells it to query the specified computer for an XDMCP login server. If successful, the result should be a connection that looks very much like a local login, although it won't be as fast—all the display data must pass over the network after all.

In addition to *-query*, X supports two other XDMCP options: *-broadcast* and *-indirect server*. The *-broadcast* option starts an XDMCP broadcast, in which the XDMCP client (that is, the X server) sends a broadcast to the local network looking for XDMCP servers. The XDMCP client then either connects to the first server it finds or presents a list to the user. (In practice, Xorg-X11 and XFree86 seem to do the former, but some X servers do the latter.) The *-indirect server* option relies on the named server computer to present a list of XDMCP servers on the network.

> **TIP** Sometimes one of these three connection methods works when the others don't, so if you have problems, you should try all three methods.

If you want to permanently configure a computer as an *X terminal* (that is, a computer that functions only as an X server for remote computers, with few local programs running aside from the X server itself), you should locate whatever script starts X running on your system and change it. This script is likely to be a *SysV* startup script, as described in Chapter 4. Sometimes this script includes X options, such as *-nolisten tcp*, that interfere with X accepting remote connections, so you may need to remove such lines. (The preceding section, “Using X Programs Remotely,” provides additional information on such configurations.)