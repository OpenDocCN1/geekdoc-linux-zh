# X server running on a Windows computer

server implementations now exist for almost every operating system. X itself is OS agnostic, as X11 clients running on a UNIX box can display display on an X server running under Microsoft Windows and still be controlled as if the user were sitting at the system console.

Unfortunately, the original designers of the X protocols did not devote much thought to security. Every program that connects to your X server can read everything you type on the keyboard and everything displayed on your screen. To make matters worse, remote programs can simply lurk silently in the background when accessing your X server; they can

Several methods of considering X11 have been proposed over time, but they have all tended to be somewhat complex. The bottom line is that by allowing remote connections to your X server unless you are absolutely sure of what you are doing. Most X servers are configured to refuse remote connections by default, so you should be safe as long as you do not run the xhost (or its equivalent) to grant remote access

Unfortunately, granting remote access is exactly what you need to do when you seek to run programs on UNIX and their interfaces on Windows. So, how to run a remote application without granting remote access to the X server? The most common method is to use a feature of the SSH protocol that is specifically designed to support X11. This scheme creates a secure tunnel between clients running on the remote host and the local X server. Programs started on the remote host display automatically on the local machine, but through the magic of SSH, the X server perceives them as having originated locally.

Note that X forwarding only works if the X forwarding features have been enabled on both the SSH server and the SSH client. If you use PuTTY SSH client on Windows, simply activate the X11 forwarding feature in its setup. On the X server side (that is, the X11 client side; the UNIX machine), make sure that the /etc/ssh/sshd_config file contains the line

X11Forwarding yes

If you modify the SSH server configuration, make sure to restart the sshd process to activate the new configuration. The X11Forwarding option is enabled by default on most UNIX systems that use OpenSSH.

As our technical reviewer Dan Foster, forwarding X connections over SSH "can be excruciating slow, even over a LAN, and it is even worse if there is any network latency." VNC, discussed below, is an alternative.

Although Apple provides a free server for Mac OS, Microsoft unfortunately offers no corresponding feature. A free server for Windows is available from the Cygwin project (cywin.com), and it works well once you've configured it. The Xming server for Windows is an excellent alternative that's much easier to configure. Commercial servers for Windows would include Exceed and X-Win32. These offer much simpler configuration at a rather steep price.

See page 926 for more information about SSH.

![](bbox=[0.943, 0.725, 0.999, 0.843])