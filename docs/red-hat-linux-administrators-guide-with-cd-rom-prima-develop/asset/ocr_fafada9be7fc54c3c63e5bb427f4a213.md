By pressing Ctrl-Alt-+ (for higher resolution) or Ctrl-Alt-– (for lower resolution), you can alternate modes and switch from a 640 × 480 display to a higher resolution on the fly from within X Window. This will move the display to a higher resolution and then rotate back through the lower settings. For systems with better video cards or larger monitors, you can set up a host of different resolutions and change settings at will.

# ## Starting X

After properly configuring X Window, you can boot into the X Window environment. The standard method of bringing up the GUI is to enter the following on the command line if you are not already at a GDM display:

```
startx
```

This is the method for users who normally log in to the system at run level 3. Several additional options are available with the initial command. If you configured your XFree86 settings correctly—that is, if you added more than one resolution setting and color depth—you should be able to start in different color modes. For instance, if you had the default depth set for 8-bit mode and wanted to boot instead into 16-bit mode, you would use the following options with startx:

```
startx -- -bpp 16
```

This brings up the color depth as 16-bit rather than 8-bit. Because you are passing a different argument to the server, the statement must be prefixed with two dashes and the bits-per-pixel setting must also have a single hyphen affixed before it. Rotating through the resolution options again requires pressing Ctrl-Alt-+ or Ctrl-Alt--.

The startx command first looks for an .xinitrc file in that user’s home directory. This is where you can set the default window manager type. If there is no .xinitrc file, the default Red Hat Linux install creates an .Xauthority file in which it stores information about the default window manager and the setup. As of the most current Red Hat release, the window manager launched by default, if no specific one is chosen during the installation, is the sawfish window manager. GNOME provides additional utilities such as the panel as well as GNOME-based programs. GNOME is actually a collection of daemons, protocols and utilities that make up the desktop environment. Sawfish controls the window functions and appearances.