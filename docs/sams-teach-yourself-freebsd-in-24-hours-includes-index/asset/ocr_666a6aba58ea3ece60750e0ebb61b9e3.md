monitor can support. Use the Ctrl+Alt+Backspace key combination mentioned earlier to exit X and restart the xf86config program—this time making sure that you enter refresh rates that your monitor can handle.

![](bbox=[0.22, 0.3, 0.28, 0.4])

> If your screen appears garbled or if you hear a high pitched whine coming from your monitor, immediately press the Ctrl+Alt+Backspace key combination to kill the X Window System. Either one of these is a sign that your monitor is trying to run a refresh rate that it can't handle. A high pitched whine especially indicates that your monitor is about ready to destroy itself. If you leave it in this state much longer, it might even start smoking.

To exit from X and return to the command prompt, hold down the left mouse button on a blank area of the desktop. A menu will pop up, and one of the options will be Exit. Move the mouse pointer over this option and release the mouse button. X should exit, and you should be returned to the command prompt.

# Summary

In this hour, you learned that the X Window System is a system that provides a graphical user interface to FreeBSD similar to that of Windows. You also learned the basic differences between X and a window manager, and learned that they work together to provide you with a working environment that can actually be used productively. You saw that X configuration is handled by the file XF86Config, and that you can use the xf86config program to build this configuration file for you. Finally, you learned how to start X and exit from the default twm window manager.

# Q&A

**Q** Where can I obtain a complete list of the video cards that XFree86 supports?
**A** An up-to-date list of supported video hardware can be obtained from the XFree86 projects Web site at the following address:
http://www.xfree86.org/current/Status.html

**Q** What is the difference between X and a window manager?
**A** X provides a framework for running a graphical user interface on FreeBSD. The window manager runs on top of X and is what provides the actual functionality for the user.