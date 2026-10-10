+   5. What is an advantage of a font server?
+   A. It provides faster font displays than are otherwise possible.
+   B. It can simplify font maintenance on a network with many X servers.
+   C. It’s the only means of providing TrueType support for XFree86 4.x.
+   D. It enables the computer to turn a bitmapped display into an ASCII text file.

+   6. What methods do Linux distributions use to start X automatically when the system boots? (Select all that apply.)
+   A. Start an XDMCP server from the Start folder
+   B. Start an XDMCP server from an `~/.xinitrc` script
+   C. Start an XDMCP server via a SysV startup script
+   D. Start an XDMCP server from `init`

+   7. How would you change the text displayed by XDM as a greeting?
+   A. Click Configure ▸ Greeting from the XDM main menu, and edit the text in the resulting dialog box.
+   B. Edit the `/etc/X11/xdm/Xresources` file, and change the text in the `xlogin*greeting` line.
+   C. Edit the `/etc/X11/xorg.conf` file, and change the `Greeting` option in the `xdm` area.
+   D. Run `xdmconfig`, and change the greeting on the Login tab.

+   8. Which of the following features do KDM and GDM provide that XDM doesn’t?
+   A. An encrypted remote X-based access ability, improving network security
+   B. The ability to accept logins from remote computers, once properly configured
+   C. The ability to select the login environment from a menu on the main login screen
+   D. A login screen that shows the username and password simultaneously rather than sequentially

+   9. Which of the following commands tells the X server to accept connections from `penguin.example.com`?
+   A. `xhost +penguin.example.com`
+   B. `export DISPLAY=penguin.example.com:0`
+   C. `telnet penguin.example.com`
+   D. `xaccess penguin.example.com`