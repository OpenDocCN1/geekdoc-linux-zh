There are a few things you can do if the load average is too high:

+   • Make sure you are not running a screensaver. No server machine should have a screensaver going, especially fancy ones that require a lot of math. This just takes up CPU time.
+   • Shut off the GUI when you are not actively using the machine. If you use the box rarely, this can be enough to make a significant performance difference.
+   • Shut off fancy GUI features, such as animation and sounds.
+   • Change to less processor-intensive GUI components. For example, consider the following window managers, all available at [www.themes.org](http://www.themes.org): BlackBox, FVWM, IceWM, Window Maker, and wm2.
+   • Add additional RAM to the machine.
+   • Remove the GUI completely, because the machine just cannot handle it while also handling its services.

# # The Files

There are a number of files used by the X Window System, GNOME, and KDE. Trying to figure out how and when these files are used, and which they should turn to when changing systemwide or personal GUI configurations, leads many users into immense frustration and hours of Web searching. Although I have tried to address as many specific needs as I can think of in the Immediate Solutions portion of this chapter, this section includes listings of the configuration files used by X, GNOME, and KDE.

# ## The X Window System Files

There is some variation between distributions when it comes to where to find some X files. However, which files are used for what is fairly standardized across distributions. The confusing part to the X files is that which files you alter depends on how you enter the GUI. In this section, I refer to booting into the GUI, and starting it by hand. Booting refers to having your system set to enter the GUI by default. Starting it by hand means the system boots to the command line and you use the **startx** command to enter X.

Some files are important regardless of how you enter the GUI:

+   • /etc/X11/XF86Config—The primary X configuration file for your machine's hardware.
+   • /usr/X11R6/lib/X11/fonts/—Directory containing a series of subdirectories that hold all of the X fonts.
+   • /usr/X11R6/lib/X11/app-defaults/—Directory containing configuration files for the various applications available in X, and what states they will open into.

6. GUI Management