# Review Questions

+   4. In what section of XF86Config or xorg.conf do you specify the resolution that you want to run?

+   A. In the ServerLayer section, using the Screen option

+   B. In the Monitor section, using the Modeline option

+   C. In the Device section, using the Modeline option

+   D. In the DefaultResolution section, using the Define option

+   E. In the Screen section, subsection Display, using the Modes option

+   5. What is an advantage of a font server?

+   A. It provides faster font displays than are otherwise possible.

+   B. It can simplify font maintenance on a network with many X servers.

+   C. It's the only means of providing TrueType support for XFree8 86.4.

+   D. It enables the computer to turn a bitmap display into an ASCII text file.

+   E. It enables X to use font smoothing, which isn't possible with core fonts.

+   6. What methods Linux distributions use to start X automatically when the system boots? (Select two.)

+   A. Start an XDMCP server from the Start folder.

+   B. Start an XDMCP server from ~/.xinitrc script.

+   C. Start an XDMCP server via a system startup script.

+   D. Start an XDMCP server via a boot manager.

+   E. Start an XDMCP server from init.

+   7. How would you change the text displayed by KDM as a greeting?

+   A. Click Configure > Greeting from the KDM main menu, and edit the text in the resulting dialog box.

+   B. Pass "text" as a kernel option in the boot loader, changing text to the new greeting.

+   C. Edit the /etc/X11/xorg.conf file, and change the Greeting in the xdm area.

+   D. Run xdmconfig, and change the Greeting on the Login tab.

+   E. Edit the /etc/X11/xdm/resources file, and change the text in the login-greeting line.

+   8. Which of the following features KDM and GDM provide that XDM does not?

+   A. An encrypted remote X-based access ability, improving network security

+   B. The ability to accept logins from remote computers, once properly configured

+   C. The ability to select the login environment from a menu on the main login line

+   D. A login screen that shows the username and password simultaneously rather than sequentially

+   E. An option to log into text mode if X should fail to start