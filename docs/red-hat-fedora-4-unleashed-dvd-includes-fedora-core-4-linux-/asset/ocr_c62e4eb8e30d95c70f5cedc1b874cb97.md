```
FontPath "\usr/X11R6/lib/X11/fonts/75dpi"
FontPath "\usr/X11R6/lib/X11/fonts/type1"
FontPath "\usr/X11R6/lib/X11/fonts/Speedo"
...
```

These directories contain the default compressed fonts that are available for use during the X session. The font server is configured by using the file named config under the /etc/X11/fs directory. This file contains a listing, or catalog, of fonts for use by the font server. By adding an alternate-server entry in this file and restarting the font server, you can specify remote font servers for use during X sessions. This can help centralize font support and reduce local storage requirements (even though only 25MB is required for the almost 5,000 fonts installed with Red Hat Linux and X).

# The Module Section

The Module section of the xorg.conf file specifies loadable modules or drivers to load for the X session. This section might look like this:

```
Section "Module"
    Load "dbe"
    Load "extmod"
    Load "fbdevhw"
    Load "glx"
    Load "record"
    Load "freetype"
    Load "type1"
    Load "dri"
EndSection
```

These modules can range from special video card support to font rasterizers. The modules are located in subdirectories under the /usr/X11R6/lib/modules directory.

# The InputDevice Section

The InputDevice section configures a specific device, such as a keyboard or mouse, as in this example:

```
Section "InputDevice"
    Identifier "Keyboard0"
    Driver "kbd"
    Option "XkbModel" "pc105"
    Option "XkbLayout" "us"
EndSection
Section "InputDevice"
    Identifier "Mouse0"
    Driver "mouse"
    Option "Protocol" "IMPS/2"
```