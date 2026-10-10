# Chapter 21: Login Servers

At this point, the VNC server should respond to queries from other computers to its session 0—for instance, **vncviewer buntan:0**. When you type such a command, or use the equivalent connection options from a Windows or Mac OS VNC viewer, VNC won't prompt for a password. Instead, you'll see your XDMCP login prompt, just as if you'd used an X server's XDMCP client. You can then use the login session much as you would a local login or a root X login.

Some of the details you set in Steps 1 and 2 are extremely important. The port number you choose to specify in `/etc/services` determines the session number you use to connect to the VNC server. Port 5900 corresponds to session 0, 5901 corresponds to session 1, and so on. The `-1` option in the `inetd.conf` file determines the X session number that VNC occupies. If X is running locally, it probably occupies session 0, which is why this example uses `-1`. If you don't run X locally, you can omit this option, and VNC will try to use session 0. The `-inetd` option tells VNC that it's running from `inetd`, and the `-once` option tells VNC to stop running when the session terminates, which is necessary in an `inetd` configuration. The `-query localhost` option works just like the same option would in an ordinary X server; it links the X server to the XDMCP server running on the local computer.

> If you try this configuration and VNC doesn't respond as you expect, try typing **telnet vncserver 5900**, where vncserver is the VNC server computer. This command should show you error messages that may help diagnose the problem. For instance, if VNC is trying to use an X session that you've already in use, you'll see an error message to that effect when you use `telnet` to connect to the VNC port.

Using `inetd` to launch VNC changes many of the features that make VNC unique:

+   - VNC sessions are no longer persistent; if you terminate a VNC session, you must log in again, and if you terminate a session without first logging out, your programs will exit, so you might lose work. Similarly, two users cannot connect to the same VNC desktop.
+   - The VNC server accepts multiple logins to the same VNC session number.
+   - There's no need for users to log in and explicitly launch a VNC server; it's always available.
+   - Logins use whatever login scripts the XDMCP server runs, not the `~/ .vnc/xstartup` file.
+   - Authentication isn't based on the user's VNC password; it's based on the usual FreeBSD username and password. One negative consequence of this feature is that the password isn't encrypted, as it is during VNC's normal password exchange.

On the whole, running VNC from `inetd` is a good approach for a multiuser computer or if you want a remote-access method that works more like a remote X server, but without the hassles of X server configuration. This approach places the bulk of the