using your notebook as a server, you'll probably want to benefit from the graphics features of your laptop's display. The good news is that X11 works on just about every laptop ever made. How well X11 works depends on how well X is supported by your notebook's graphics chipset.

Getting the most out of your notebook's display with the XFree86 software is a combination of several factors. First, your notebook's graphics chipset should be supported by the XFree86 software. Next, you need to craft a correct XF86Config file, which is usually located under the /etc/X11 directory (or /usr/X11R6/lib/X11 or /root if you're testing X as the root operator).

The XF86Config file settings are critical to having a properly configured graphical interface. This file contains various sections dealing with the following:

+   - Locations of installed fonts and other files
+   - Settings and options for the X server
+   - Keyboard configuration and mappings of various keys
+   - Pointer settings, such as type, speed, or number of buttons
+   - Correct horizontal and vertical frequency settings of your notebook's LCD display
+   - Specifications, such as the amount of video RAM and options for your notebook's graphics chipset
+   - Lists of available resolutions and color depths for your notebook
+   - Options specifying what color depth and resolution to use by default

The format and content of the XF86Config file are documented in its man page, which you can read with the man command like this:

```
$ man XF86Config
```

Scroll through the document and press the Q key when finished. You should also read the file QuickStart.doc under the /usr/X11R6/lib/X11/doc directory when trying to manually configure X11.

If you cannot get your display configured during your Linux installation, don't worry! Every Linux distribution, including Red Hat, Mandrake, and Yellow Dog Linux, comes with two or more utilities you can use to configure your display. Each utility is designed to build a working XF86Config file for your notebook and X11.