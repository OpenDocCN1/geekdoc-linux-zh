# TABLE 11.5 Common rdesktop Options

| Command Name | Effect |
| :--- | :--- |
| -u username | Specify a username for accessing the server. |
| -d domain | Specify a domain for accessing the server. |
| -s shell | Start the specified program rather than Explorer on the server. |
| -p password | Pass the specified password to the server. This may have no effect if the Alwavs Prompt for Password option is set on the server. |
| -g geometry | Specify the desktop size; geometry is specified as width and height, separated by an x, as in 1024x768. |
| -f | Enter full-screen mode. |
| -a bitdepth | Specify the color depth (8, 15, 16, or 24). Depths greater than 8 work only with Windows XP or newer. |

# ## Using VNC

VNC’s greatest strength is its cross-platform nature. VNC clients and servers are available for Linux, other Unix variants, Mac OS, Windows, and more obscure O/Ss. This makes VNC a good choice for remote GUI access in a cross-platform environment.

# ### Configuring a VNC Server

The standard VNC server configuration on Linux is rather odd: it runs the VNC server as an ordinary user. Accessing the server produces a login to the computer as the user who ran the server. Thus, if Fred and Mary both run VNC servers on a Linux system, each can log in separately; but if George and Sally also have accounts on the system but don’t run VNC, they won’t be able to log in remotely. Behind the scenes, VNC server programs for Linux include both a VNC server and an X server; the two are linked, with the VNC server half functioning as a virtual keyboard, mouse, and monitor for the X server half.

![](bbox=[0.15, 0.81, 0.22, 0.86])

It’s possible to link VNC to an X Display Manager Control Protocol (XDMCP) server. When this is done, users who access the VNC server system will see a standard Linux XDMCP login screen. This configuration requires using advanced VNC options that aren’t described here.