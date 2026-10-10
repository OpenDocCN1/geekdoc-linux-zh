root tty2 Jul 24 07:19
lena tty3 Jul 23 22:24
lena 0: Jul 25 22:03

lenny -> uname -n
magrat.example.com

# 10.4.4.2 X11 and TCP forwarding

If the X11Forwarding entry is set to yes on the target machine and the user is using X applications, the DISPLAY environment variable is set, the connection to the X11 display is automatically forwarded to the remote side in such a way that any X11 programs started from the shell will go through the encrypted channel, and the connection to the real X server will be made from the local machine. The user should not manually set DISPLAY. Forwarding of X11 connections can be configured on the command line or in the sshd configuration file.

The value for DISPLAY set by ssh will point to the server machine, but with a display number greater than zero. This is normal, and happens because ssh creates a proxy X server on the server machine (that runs the X client application) for forwarding the connections over the encrypted channel.

This is all done automatically, so when you type in the name of a graphical application, it is displayed on your local machine and not on the remote host. We use xclock in the example, since it is a small program which is generally installed and ideal for testing:

![](bbox=[0.13, 0.56, 0.78, 0.91])