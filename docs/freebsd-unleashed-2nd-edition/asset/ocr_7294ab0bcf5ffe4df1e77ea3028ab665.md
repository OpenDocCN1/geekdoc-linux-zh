> **TIP**
> If you are connecting to the remote system by using an X-Server running on Windows, make sure you use the Telnet or SSH application included with your X-Server software. Because the Windows Telnet application knows nothing about the X-Server, it does not work correctly for the procedures described in the following sections.

# ### Starting a Remote Application

To start an application on the remote host and have it display its output on the local system, you need to set the DISPLAY environment variable on the remote host to your local system. You can do this from the Telnet, SSH, or rlogin session. In your connection window to the remote host, you can usually use something like the following to start a remote application and display it on your system (this example assumes that your local host is named simba):

```
bash$ DISPLAY=simba:0; export DISPLAY
bash$ xcalc &
```

This code is for a Bourne-style shell (that is, bourne, korn, or bash). If you are using a C shell (or tcsh), replace the first line with the following:

```
% setenv DISPLAY simba:0
```

This code should start an xcalc on the remote host and display the output on your screen.

The DISPLAY environment variable has the following syntax:

```
DISPLAY=hostname:display#:screen#
```

Here, *display*# is almost always set to 0, and you can usually eliminate *screen*# unless you are on a system that has multiple screens attached to it.

> **TIP**
> Make sure you enter the information in the Telnet or SSH window that is connected to the remote host. Entering the information on a local xterm window will not have the desired effect.

# ### Other Client Access Controls

There are other ways to control which hosts can display applications on the local host. Some of these ways are more secure than using the xhost method described previously. The other methods and their configuration are beyond the scope of this book. However, you might want to read the man page for Xsecurity to get you started. (Note that this is case-sensitive when you try to access the man page.)