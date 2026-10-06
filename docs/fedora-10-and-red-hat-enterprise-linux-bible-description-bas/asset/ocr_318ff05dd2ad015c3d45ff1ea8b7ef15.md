# Chapter 3: Getting Started with the Desktop 135

+   - Slide windows around — Press and hold the mouse button, and then press the left, right, up, or down arrow keys to slide the current window around the screen.

If you tired of wobbling windows and spinning cubes, turning off the AIGLX 3D effects and returning Metacity as the window manager can be quite simple. Just select System -> Preferences -> Look and Feel -> Desktop Effects again and toggle the Enable Desktop Effects to turn off the feat.

If you have a supported video card, but find that you are not able to turn on the Desktop Effects, check that your X server started properly. In particular, make sure that your /etc/X11/xorg.conf file is properly configured. Make sure that glx are loaded by the Module section. Also, add an extension that appears as:

```
Section "extensions"
Option "Composite"
EndSection
```

Another option is to add the following line to the /etc/X11/xorg.conf file in the Device section:

```
Option XANooOffscreenPmaps
```

The XANooOffscreenPmaps option will improve performance.
Check your /var/log/xorg.0 file to make sure that DRI and AIGLX features are started correctly. The messages in that file can help you debug other problems as well.

# Using the Xfce Desktop Environment

The Xfce desktop environment provides a lightweight interface for using your Fedora or RHEL system. Because it is designed to conserve system resources and load applications quickly

To meet its goals of running fast and efficiently, Xfce offers its applications for many desktop operations. Here are some examples:

+   - Thunar File Manager — A fast and efficient way of managing your files and folders.
- Xfce Application Finder — A useful tool for finding every desktop-ready application on the system. (From the Xfce menu, select Accessories -> Appfinder).
- Xfce Settings Manager — Provides tools for changing desktop, display, file manager, keyboard, mouse, and various other desktop settings. (From the Xfce menu, select Settings -> Settings Manager.)
- Mousepad — A simple and efficient text editor.